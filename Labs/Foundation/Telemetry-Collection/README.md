# Foundation — Telemetry Collection

## Objetivo

Implementar la recolección de telemetría desde los diferentes sistemas del laboratorio hacia **Wazuh SIEM**, garantizando la disponibilidad de eventos necesarios para actividades de **Security Monitoring**, **Threat Hunting**, **Detection Engineering** e **Incident Response**.

---

## Alcance

Este laboratorio contempla la incorporación de endpoints al SIEM y la validación de la generación, transmisión, procesamiento e indexación de eventos de seguridad.

Incluye:

- registro de agentes Wazuh;
- configuración de Windows y Linux;
- validación de conectividad;
- recepción de eventos;
- procesamiento por Wazuh Manager;
- almacenamiento e indexación en Wazuh Indexer;
- visualización desde Wazuh Dashboard;
- verificación de telemetría.

No contempla el desarrollo de reglas personalizadas ni investigaciones avanzadas, actividades documentadas en laboratorios posteriores.

---

## Arquitectura

Cada endpoint utiliza su propio **Wazuh Agent**. Los agentes envían los eventos al **Wazuh Manager**, donde son procesados por el Analysis Engine. Los eventos y alertas son posteriormente enviados al **Wazuh Indexer** para su almacenamiento e indexación y pueden ser consultados desde **Wazuh Dashboard**.

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
              Analysis Engine
                    │
                    ▼
              Wazuh Indexer
                    │
                    ▼
              Wazuh Dashboard
```

---

## Tecnologías utilizadas

### SIEM

- Wazuh.

### Sistemas operativos

- Windows 11.
- Ubuntu.

### Agentes

- Wazuh Agent.

### Telemetría Windows

- Windows Event Logs.
- Sysmon.

### Telemetría Linux

- auditd.
- Syslog.
- systemd journal, consultado mediante `journalctl`.

---

## Requisitos

Antes de iniciar este laboratorio se verificó:

- Wazuh Manager operativo;
- Wazuh Indexer operativo;
- Wazuh Dashboard accesible;
- comunicación entre equipos;
- resolución DNS;
- sincronización horaria;
- conectividad de red.

---

## Implementación

Las principales actividades realizadas fueron:

1. Instalación del Wazuh Agent en Windows.
2. Instalación del Wazuh Agent en Ubuntu.
3. Registro de los agentes.
4. Configuración del archivo `ossec.conf` cuando correspondía.
5. Configuración de fuentes de eventos.
6. Reinicio controlado de servicios.
7. Validación de comunicación con Wazuh Manager.
8. Confirmación del estado de los agentes.
9. Verificación de eventos y alertas en el Dashboard.

---

## Configuración

### Windows

Se configuraron y validaron:

- Wazuh Agent;
- Windows Event Logs;
- Sysmon.

### Ubuntu

Se configuraron y validaron:

- Wazuh Agent;
- auditd;
- Syslog;
- systemd journal, consultado mediante `journalctl`.

---

## Flujo de telemetría

```text
Evento generado
      │
      ▼
Fuente de telemetría
      │
      ▼
Wazuh Agent
      │
      ▼
Wazuh Manager / Analysis Engine
      │
      ▼
Wazuh Indexer
      │
      ▼
Wazuh Dashboard
```

El Manager procesa la información y aplica la lógica de detección; el Indexer almacena e indexa los datos; el Dashboard permite su consulta y análisis.

---

## Validación

Se verificó:

- agentes conectados;
- estado `Active`;
- recepción continua de eventos;
- procesamiento por el Manager;
- indexación de información;
- visualización desde Wazuh Dashboard;
- consistencia de timestamps y contexto del evento.

---

## Problemas encontrados y troubleshooting

Durante la implementación pueden presentarse situaciones como:

- agentes desconectados;
- configuración incorrecta del Manager;
- errores de certificados;
- bloqueo de puertos o Firewall;
- desincronización horaria;
- errores de configuración del agente;
- problemas de permisos o lectura de fuentes de logs.

Las validaciones utilizadas para resolver incidencias incluyeron:

- revisión de `ossec.conf`;
- verificación de servicios;
- revisión de logs;
- reinicio controlado del agente;
- comprobación de conectividad;
- verificación desde Wazuh Dashboard.

---

## Evidencia

Este laboratorio documenta:

- registro y estado de agentes;
- conectividad;
- configuración de fuentes de telemetría;
- eventos recibidos;
- alertas generadas cuando corresponde;
- validación de procesamiento e indexación;
- capturas o evidencias técnicas obtenidas durante las pruebas.

---

## Detecciones implementadas

No aplica como objetivo principal.

En esta etapa se valida la correcta generación y recepción de telemetría. Las validaciones y reglas específicas se documentan en **Detection Engineering**.

---

## Mapeo MITRE ATT&CK

No aplica de forma directa a la infraestructura de recolección. El mapeo se realiza sobre comportamientos, detecciones e investigaciones concretas.

---

## Lecciones aprendidas

- La calidad del monitoreo depende directamente de la calidad de la telemetría.
- Cada endpoint requiere su propia ruta de recolección y agente.
- Wazuh Manager procesa la información; Wazuh Indexer la almacena e indexa.
- La validación temprana de conectividad y tiempo evita errores de correlación.
- La telemetría debe validarse antes de desarrollar detecciones o Threat Hunting.

---

## Referencias

- Wazuh Documentation.
- Microsoft Sysmon Documentation.
- Microsoft Learn.
- Linux auditd Documentation.
