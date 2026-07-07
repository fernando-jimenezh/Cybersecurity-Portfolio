# Security Monitoring - Linux Telemetry

## Objetivo

Implementar y validar la recolección de telemetría en sistemas Linux mediante **Wazuh Agent**, **auditd**, **Syslog** y **Journalctl**, garantizando la disponibilidad de eventos para las actividades de **Security Monitoring**, **Threat Hunting**, **Detection Engineering** e **Incident Response**.

---

# Alcance

Este laboratorio contempla la incorporación de un endpoint Linux al entorno de monitoreo y la validación de sus principales fuentes de eventos.

Incluye:

- Instalación de Wazuh Agent.
- Configuración de auditd.
- Configuración de Syslog.
- Validación de Journalctl.
- Verificación de conectividad con Wazuh.
- Confirmación de recepción de eventos.

No contempla la creación de reglas de detección ni investigaciones de seguridad.

---

# Arquitectura

```
Ubuntu
   │
   │ auditd
   │ Syslog
   │ Journalctl
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

La telemetría generada en el sistema Linux es enviada al **Wazuh Manager**, donde es analizada, indexada y visualizada desde el **Dashboard**.

---

# Tecnologías Utilizadas

## Sistema Operativo

- Ubuntu

## Herramientas

- Wazuh Agent
- auditd
- Syslog
- Journalctl
- Bash

---

# Requisitos

Antes de iniciar este laboratorio se verificó:

- Wazuh Manager operativo.
- Agente Linux registrado.
- Comunicación con el servidor.
- Resolución DNS.
- Sincronización horaria.

---

# Implementación

Las principales actividades realizadas fueron:

1. Instalación del agente Wazuh.
2. Registro del endpoint Linux.
3. Configuración de auditd.
4. Validación de Syslog.
5. Verificación de Journalctl.
6. Reinicio de servicios.
7. Confirmación de recepción de eventos.

---

# Configuración

## Wazuh Agent

Configuración del agente para establecer comunicación con el **Wazuh Manager**.

---

## auditd

Configuración del servicio de auditoría para registrar eventos relacionados con:

- Acceso a archivos.
- Cambios de permisos.
- Ejecución de comandos.
- Actividad de usuarios.
- Procesos.

---

## Syslog

Configuración para el almacenamiento y envío de eventos del sistema operativo.

---

## Journalctl

Validación de eventos generados por los diferentes servicios del sistema.

---

# Validación

Se verificó:

- Estado del agente.
- Comunicación con el Manager.
- Recepción de eventos.
- Visualización desde el Dashboard.
- Integridad de la telemetría.

---

# Evidencias

Las evidencias documentadas incluyen:

- Estado del agente.
- Configuración de auditd.
- Configuración de Syslog.
- Eventos recibidos.
- Capturas del Dashboard.
- Validación de conectividad.

Las capturas de pantalla y evidencias serán incorporadas durante el desarrollo del laboratorio.

---

# Detecciones Implementadas

En esta etapa únicamente se valida la correcta recepción de la telemetría del sistema Linux.

Las reglas de detección serán implementadas en laboratorios posteriores.

---

# Mapeo MITRE ATT&CK

La telemetría obtenida en este laboratorio permite identificar actividades relacionadas con técnicas de:

- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Discovery

El mapeo específico será desarrollado durante los ejercicios de **Threat Hunting** y **Detection Engineering**.

---

# Aplicación en un Entorno Empresarial

Las actividades desarrolladas en este laboratorio representan tareas habituales de un **SOC Analyst**, entre ellas:

- Validación del estado de los agentes.
- Supervisión de la recolección de eventos.
- Verificación de servicios críticos.
- Monitoreo de sistemas Linux.
- Confirmación de la disponibilidad de telemetría para investigaciones de seguridad.

---

# Competencias Desarrolladas

Al finalizar este laboratorio se fortalecieron las siguientes competencias:

- Administración de **Wazuh Agent**.
- Configuración de **auditd**.
- Gestión de **Syslog**.
- Análisis de **Journalctl**.
- Validación de telemetría en Linux.
- Troubleshooting de agentes.
- Security Monitoring sobre sistemas Linux.

---

# Lecciones Aprendidas

- La calidad de la telemetría depende de una correcta configuración de los servicios de auditoría.
- La validación temprana de los agentes evita pérdidas de información durante el monitoreo.
- Linux proporciona múltiples fuentes de eventos que complementan la visibilidad del entorno.
- Una correcta recolección de eventos es esencial para actividades de **Threat Hunting** e **Incident Response**.

---

# Referencias

- Ubuntu Documentation
- Linux auditd Documentation
- Wazuh Documentation
- MITRE ATT&CK
