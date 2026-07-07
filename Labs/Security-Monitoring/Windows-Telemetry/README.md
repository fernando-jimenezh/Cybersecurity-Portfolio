# Security Monitoring - Windows Telemetry

## Objetivo

Implementar y validar la recolección de eventos de seguridad en **Windows 11** mediante **Windows Event Logs**, **Sysmon** y **Wazuh Agent**, asegurando la disponibilidad de información para actividades de monitoreo, investigación y detección de amenazas.

---

# Alcance

Este laboratorio contempla la configuración de las principales fuentes de eventos de Windows utilizadas por un **SOC**.

Incluye:

- Windows Event Logs.
- Sysmon.
- Wazuh Agent.
- Validación de eventos.
- Recepción de telemetría en Wazuh.

No contempla la creación de reglas de detección, actividad que será desarrollada en laboratorios posteriores.

---

# Arquitectura

```
Windows 11
      │
      │ Windows Event Logs
      │ Sysmon
      ▼
Wazuh Agent
      │
      ▼
Wazuh Manager
      │
      ▼
Indexer
      │
      ▼
Dashboard
```

Toda la telemetría generada en el endpoint es enviada hacia Wazuh para su procesamiento y almacenamiento.

---

# Tecnologías Utilizadas

## Sistemas Operativos

- Windows 11

## Herramientas

- Wazuh Agent
- Sysmon
- Event Viewer
- PowerShell

---

# Requisitos

Antes de iniciar este laboratorio se verificó:

- Wazuh Manager operativo.
- Agente registrado.
- Comunicación con el servidor.
- Sincronización horaria.
- Acceso al Dashboard.

---

# Implementación

Las actividades realizadas fueron:

1. Instalación del agente Wazuh.
2. Instalación de Sysmon.
3. Aplicación de la configuración de Sysmon.
4. Reinicio del servicio.
5. Validación de eventos.
6. Confirmación de recepción en Wazuh.

---

# Configuración

## Windows Event Logs

Se monitorearon principalmente los registros:

- Security
- System
- Application

---

## Sysmon

Se habilitó la generación de eventos relacionados con:

- Creación de procesos.
- Conexiones de red.
- Creación de archivos.
- Carga de DLL.
- Cambios en el Registro.
- Creación de servicios.
- Tareas programadas.

---

# Eventos Relevantes

Durante este laboratorio se validó la generación de eventos como:

- Inicio y cierre de sesión.
- Ejecución de PowerShell.
- Ejecución de CMD.
- Creación de procesos.
- Conexiones de red.
- Cambios en el sistema.

Estos eventos constituyen una fuente fundamental para actividades de **Threat Hunting**.

---

# Validación

Se verificó:

- Estado del agente.
- Recepción de eventos.
- Eventos Sysmon.
- Windows Event Logs.
- Visualización desde Wazuh Dashboard.

---

# Evidencias

Las evidencias documentadas incluyen:

- Configuración del agente.
- Instalación de Sysmon.
- Eventos generados.
- Capturas del Dashboard.
- Validación de eventos.

---

# Detecciones Implementadas

En esta etapa únicamente se valida la correcta recepción de telemetría.

Las reglas personalizadas serán desarrolladas posteriormente.

---

# Mapeo MITRE ATT&CK

Este laboratorio proporciona información útil para identificar técnicas asociadas a:

- Execution
- Discovery
- Persistence
- Privilege Escalation
- Defense Evasion

El mapeo específico será realizado en los laboratorios de **Threat Hunting** y **Detection Engineering**.

---

# Aplicación en un SOC

Este laboratorio desarrolla competencias utilizadas diariamente por un **SOC Analyst**:

- Validación de telemetría.
- Verificación de agentes.
- Monitoreo de eventos.
- Identificación de anomalías.
- Confirmación de fuentes de información.
- Preparación de datos para investigaciones.

---

# Lecciones Aprendidas

- La calidad del monitoreo depende de una correcta configuración de Sysmon.
- La validación de eventos debe realizarse antes de crear reglas de detección.
- Windows Event Logs y Sysmon proporcionan información complementaria.
- La telemetría es la base para cualquier investigación de seguridad.

---

# Referencias

- Microsoft Learn
- Sysmon Documentation
- Wazuh Documentation
- MITRE ATT&CK
