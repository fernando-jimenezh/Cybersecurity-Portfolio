# Security Monitoring — Windows Telemetry

## Objetivo

Implementar y validar la recolección de eventos de seguridad en **Windows 11** mediante **Windows Event Logs**, **Sysmon** y **Wazuh Agent**, asegurando la disponibilidad de información para actividades de monitoreo, investigación y detección de amenazas.

---

## Alcance

Este laboratorio contempla la configuración y validación de las principales fuentes de telemetría utilizadas durante actividades SOC en Windows.

Incluye:

- Windows Event Logs;
- Sysmon;
- Wazuh Agent;
- validación de eventos;
- recepción y procesamiento de telemetría en Wazuh.

No contempla como objetivo principal el desarrollo de reglas de detección personalizadas.

---

## Arquitectura

```text
Windows 11
    │
    ├── Windows Event Logs
    └── Sysmon
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

Windows Event Logs y Sysmon proporcionan fuentes complementarias. Wazuh Agent recopila los eventos configurados y los envía a Wazuh Manager para su procesamiento; posteriormente se almacenan e indexan en Wazuh Indexer.

---

## Tecnologías utilizadas

- Windows 11.
- Wazuh Agent.
- Sysmon.
- Event Viewer.
- PowerShell.

---

## Requisitos

Antes de iniciar este laboratorio se verificó:

- Wazuh Manager operativo;
- agente registrado;
- comunicación con el servidor;
- sincronización horaria;
- acceso al Dashboard;
- Sysmon instalado y configurado.

---

## Implementación

Las actividades realizadas fueron:

1. Instalación del Wazuh Agent.
2. Instalación de Sysmon.
3. Aplicación de la configuración de Sysmon.
4. Configuración de Windows Event Logs relevantes.
5. Reinicio controlado de servicios cuando fue necesario.
6. Generación de eventos de prueba.
7. Confirmación de recepción en Wazuh.

---

## Configuración

### Windows Event Logs

Se monitorearon principalmente registros como:

- Security;
- System;
- Application;
- canales adicionales cuando el escenario lo requería.

Windows Event Logs proporcionan eventos de autenticación, cambios del sistema, instalación de servicios, tareas programadas y otras actividades registradas por Windows.

### Sysmon

Sysmon se utilizó para ampliar la visibilidad sobre actividades como:

- **Process Create**;
- conexiones de red, cuando están habilitadas;
- creación o modificación de archivos según la configuración;
- carga de imágenes/DLL;
- cambios en el Registro;
- otras categorías soportadas por la versión y configuración aplicada.

> La creación de servicios y de tareas programadas no corresponde a eventos específicos de Sysmon. Estas actividades se investigan principalmente mediante **Windows Event Logs** y la telemetría asociada a procesos, Registro u otras fuentes complementarias.

---

## Eventos relevantes

Durante el laboratorio se validó la disponibilidad de información relacionada con:

- inicio y cierre de sesión desde Windows Event Logs;
- ejecución de PowerShell;
- ejecución de `cmd.exe`;
- creación de procesos mediante Sysmon Event ID 1;
- conexiones de red cuando la configuración de Sysmon lo permite;
- cambios del sistema visibles mediante las fuentes configuradas.

---

## Validación

Se verificó:

- estado del agente;
- recepción de Windows Event Logs;
- recepción de eventos Sysmon;
- procesamiento por Wazuh Manager;
- visualización desde Wazuh Dashboard;
- consistencia entre evento original y datos disponibles para investigación.

---

## Evidencias

Las evidencias documentadas incluyen:

- configuración del agente;
- instalación y configuración de Sysmon;
- eventos generados;
- eventos Windows relevantes;
- capturas o registros del Dashboard;
- validación de campos utilizados posteriormente en investigaciones.

---

## Detecciones implementadas

En esta etapa se prioriza la correcta recepción de telemetría. La validación de reglas nativas y personalizadas se documenta en **Detection Engineering** y en los proyectos DR.

---

## Mapeo MITRE ATT&CK

La telemetría obtenida puede apoyar investigaciones relacionadas con **Execution**, **Discovery**, **Persistence**, **Privilege Escalation** y **Defense Evasion**. El mapeo específico se realiza únicamente sobre eventos y comportamientos concretos.

---

## Aplicación en un SOC

Este laboratorio desarrolla competencias utilizadas por un **SOC Analyst**:

- validación de telemetría;
- verificación de agentes;
- análisis de eventos;
- correlación entre Windows Event Logs y Sysmon;
- identificación de anomalías;
- preparación de evidencia para investigación.

---

## Lecciones aprendidas

- Windows Event Logs y Sysmon proporcionan visibilidad complementaria.
- La configuración de Sysmon determina qué categorías de eventos estarán disponibles.
- No debe atribuirse a Sysmon un evento que pertenece a Windows Event Logs.
- La validación de telemetría debe realizarse antes de desarrollar reglas de detección.
- La relación entre procesos es una fuente importante de contexto para Detection Engineering y Threat Hunting.

---

## Referencias

- Microsoft Learn.
- Microsoft Sysmon Documentation.
- Wazuh Documentation.
- MITRE ATT&CK.
