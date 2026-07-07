# Security Monitoring - Log Analysis

## Objetivo

Analizar los eventos de seguridad recopilados por **Wazuh SIEM** para identificar comportamientos normales y actividades potencialmente sospechosas, comprendiendo el flujo de la información desde su generación hasta su visualización en el **Dashboard**.

---

# Alcance

Este laboratorio contempla el análisis inicial de eventos provenientes de los sistemas Windows y Linux integrados al laboratorio.

Incluye:

- Exploración de eventos.
- Identificación de fuentes de logs.
- Análisis de alertas.
- Clasificación de eventos.
- Priorización de alertas.
- Validación de información registrada.

No contempla investigaciones avanzadas ni actividades de Threat Hunting.

---

# Arquitectura

```
Windows 11           Ubuntu
     │                  │
     ▼                  ▼
 Windows Logs      auditd / Syslog
          │
          ▼
      Wazuh Agent
          │
          ▼
     Wazuh Manager
          │
          ▼
     Wazuh Indexer
          │
          ▼
    Wazuh Dashboard
```

---

# Tecnologías Utilizadas

## SIEM

- Wazuh

## Sistemas Operativos

- Windows 11
- Ubuntu

## Herramientas

- Wazuh Dashboard
- Wazuh Manager
- Wazuh Indexer

---

# Requisitos

Antes de iniciar este laboratorio se verificó:

- Agentes conectados.
- Recepción de telemetría.
- Dashboard operativo.
- Indexación de eventos.
- Comunicación entre todos los componentes.

---

# Implementación

Durante este laboratorio se realizaron las siguientes actividades:

1. Acceso al Dashboard.
2. Revisión de alertas generadas.
3. Exploración de eventos.
4. Identificación de la fuente del evento.
5. Validación del agente que originó el evento.
6. Análisis de la información registrada.

---

# Configuración

Se utilizaron las vistas predeterminadas de Wazuh para consultar:

- Security Events
- Agent Events
- Authentication Events
- Sysmon Events
- Linux Events

No fue necesaria la creación de reglas personalizadas.

---

# Validación

Se verificó:

- Recepción de eventos Windows.
- Recepción de eventos Linux.
- Correcta indexación.
- Visualización desde el Dashboard.
- Integridad de los datos recibidos.

---

# Evidencias

Durante este laboratorio se documentan:

- Alertas generadas.
- Eventos recibidos.
- Información del agente.
- Nivel de severidad.
- Fecha y hora del evento.
- Fuente del log.

Las capturas y ejemplos serán incorporados posteriormente.

---

# Detecciones Implementadas

En esta etapa únicamente se realizó el análisis de eventos generados por la configuración predeterminada de Wazuh.

No se implementaron reglas de detección personalizadas.

---

# Mapeo MITRE ATT&CK

Los eventos analizados permiten identificar actividades relacionadas con tácticas como:

- Initial Access
- Execution
- Persistence
- Discovery
- Credential Access
- Defense Evasion

El mapeo detallado será desarrollado en los laboratorios de **Threat Hunting**.

---

# Aplicación en un Entorno Empresarial

El análisis de logs constituye una de las actividades principales de un **SOC Analyst**.

Las tareas realizadas en este laboratorio representan actividades habituales como:

- Revisión de alertas.
- Validación de eventos.
- Correlación de información.
- Identificación de comportamientos anómalos.
- Priorización de incidentes.
- Verificación de la calidad de la telemetría.

---

# Competencias Desarrolladas

Al finalizar este laboratorio se fortalecieron las siguientes competencias:

- Análisis de eventos de seguridad.
- Interpretación de alertas.
- Uso de Wazuh Dashboard.
- Correlación básica de eventos.
- Validación de telemetría.
- Security Monitoring.
- Documentación técnica.

---

# Lecciones Aprendidas

- La calidad del análisis depende directamente de la calidad de la telemetría.
- La correcta interpretación de los eventos permite identificar comportamientos anómalos con mayor rapidez.
- La correlación de múltiples fuentes de información mejora el contexto de una investigación.
- La revisión periódica de alertas es una actividad fundamental dentro de un SOC.

---

# Referencias

- Wazuh Documentation
- MITRE ATT&CK
- Microsoft Learn
- Ubuntu Documentation
