# Security Monitoring — Log Analysis

## Objetivo

Analizar los eventos de seguridad recopilados por **Wazuh SIEM** para identificar comportamientos esperados y actividades potencialmente sospechosas, comprendiendo el flujo de la información desde su generación hasta su consulta en **Wazuh Dashboard**.

---

## Alcance

Este laboratorio contempla el análisis inicial de eventos provenientes de sistemas Windows y Linux integrados al entorno de monitoreo.

Incluye:

- exploración de eventos;
- identificación de fuentes de logs;
- análisis de alertas;
- clasificación y priorización;
- validación de información registrada;
- correlación básica entre fuentes.

No contempla investigaciones avanzadas ni Threat Hunting profundo, que se documentan en secciones específicas.

---

## Arquitectura

Cada endpoint utiliza su propio Wazuh Agent. Los agentes convergen en Wazuh Manager y no en un agente compartido.

```text
Windows 11                         Ubuntu
    │                                 │
Windows Event Logs / Sysmon      auditd / Syslog / systemd journal
    │                                 │
    ▼                                 ▼
Wazuh Agent                       Wazuh Agent
    │                                 │
    └───────────────┬─────────────────┘
                    ▼
              Wazuh Manager
                    │
                    ▼
              Wazuh Indexer
                    │
                    ▼
              Wazuh Dashboard
                    │
                    ▼
                Log Analysis
```

---

## Tecnologías utilizadas

- Wazuh Manager.
- Wazuh Indexer.
- Wazuh Dashboard.
- Windows 11.
- Ubuntu.
- Sysmon.
- Windows Event Logs.
- auditd.
- Syslog.
- systemd journal.

---

## Requisitos

Antes de iniciar este laboratorio se verificó:

- agentes conectados;
- recepción de telemetría;
- Dashboard operativo;
- indexación de eventos;
- sincronización horaria;
- comunicación entre componentes.

---

## Implementación

Durante el laboratorio se realizaron las siguientes actividades:

1. Acceso a Wazuh Dashboard.
2. Revisión de eventos y alertas disponibles.
3. Identificación de la fuente de cada evento.
4. Validación del agente y endpoint de origen.
5. Revisión de timestamps, severidad y campos técnicos.
6. Correlación básica con eventos relacionados.
7. Clasificación inicial de la actividad observada.

---

## Análisis

Las vistas y búsquedas disponibles en Wazuh se utilizaron para revisar información de seguridad proveniente de Windows y Linux.

El análisis diferencia entre:

- **evento:** registro generado por una fuente de telemetría;
- **alerta:** resultado producido cuando el Analysis Engine de Wazuh aplica una regla y se cumplen sus condiciones;
- **hallazgo:** conclusión obtenida después de analizar evidencia y contexto.

Esta separación evita interpretar automáticamente cada evento como una amenaza.

---

## Validación

Se verificó:

- recepción de eventos Windows;
- recepción de eventos Linux;
- correcta indexación;
- visualización desde el Dashboard;
- asociación con el endpoint correspondiente;
- consistencia de datos y timestamps.

---

## Evidencias

Durante este laboratorio se documentan, cuando corresponde:

- eventos recibidos;
- alertas generadas;
- información del agente;
- nivel de severidad;
- fecha y hora;
- fuente del log;
- campos utilizados para contextualizar la actividad.

---

## Detecciones implementadas

En esta etapa se analizó principalmente el contenido disponible mediante la configuración y reglas existentes de Wazuh. El desarrollo y validación específica de reglas se documenta en **Detection Engineering**.

---

## Mapeo MITRE ATT&CK

MITRE ATT&CK se utiliza únicamente cuando un evento, alerta o comportamiento concreto permite establecer una relación técnica justificable. La presencia de un evento por sí sola no implica que una técnica ATT&CK haya sido ejecutada de forma maliciosa.

---

## Aplicación en un entorno empresarial

El análisis de logs constituye una actividad habitual de un **SOC Analyst** e incluye:

- revisión y contextualización de alertas;
- validación de eventos;
- correlación de información;
- identificación de comportamientos anómalos;
- priorización;
- verificación de calidad de telemetría;
- documentación basada en evidencia.

---

## Competencias desarrolladas

- Análisis de eventos de seguridad.
- Interpretación de alertas.
- Uso de Wazuh Dashboard.
- Correlación básica de eventos.
- Validación de telemetría.
- Security Monitoring.
- Documentación técnica.

---

## Lecciones aprendidas

- Evento, alerta y hallazgo no son conceptos equivalentes.
- Cada endpoint mantiene su propio Wazuh Agent.
- La calidad del análisis depende de la calidad y contexto de la telemetría.
- La correlación entre múltiples fuentes mejora la investigación.
- Las conclusiones deben derivarse de evidencia y no únicamente de la severidad de una alerta.

---

## Referencias

- Wazuh Documentation.
- MITRE ATT&CK.
- Microsoft Learn.
- Ubuntu Documentation.
