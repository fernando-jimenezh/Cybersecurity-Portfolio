# Security Monitoring — Linux Telemetry

## Objetivo

Implementar y validar la recolección de telemetría en sistemas Linux mediante **Wazuh Agent**, **auditd**, **Syslog** y **systemd journal**, asegurando la disponibilidad de eventos para actividades de **Security Monitoring**, **Threat Hunting**, **Detection Engineering** e **Incident Response**.

---

## Alcance

Este laboratorio contempla la incorporación de un endpoint Linux al entorno de monitoreo y la validación de sus principales fuentes de eventos.

Incluye:

- instalación y registro de Wazuh Agent;
- configuración de auditd;
- validación de Syslog;
- revisión del systemd journal mediante `journalctl`;
- verificación de conectividad con Wazuh;
- confirmación de recepción y visualización de eventos.

No contempla la creación de reglas personalizadas ni investigaciones avanzadas.

---

## Arquitectura

```text
Ubuntu
   │
   ├── auditd
   ├── Syslog
   └── systemd journal
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

La telemetría del endpoint es recopilada por Wazuh Agent y enviada a Wazuh Manager para su procesamiento. Posteriormente, los datos son almacenados e indexados en Wazuh Indexer y pueden ser consultados desde Wazuh Dashboard.

---

## Tecnologías utilizadas

- Ubuntu.
- Wazuh Agent.
- auditd.
- Syslog.
- systemd journal.
- `journalctl` como herramienta de consulta.
- Bash.

---

## Requisitos

Antes de iniciar este laboratorio se verificó:

- Wazuh Manager operativo;
- agente Linux registrado;
- comunicación con el servidor;
- resolución DNS;
- sincronización horaria;
- permisos adecuados para las fuentes de eventos.

---

## Implementación

Las principales actividades realizadas fueron:

1. Instalación del Wazuh Agent.
2. Registro del endpoint Linux.
3. Configuración de auditd.
4. Validación de Syslog.
5. Revisión del systemd journal mediante `journalctl`.
6. Reinicio controlado de servicios cuando fue necesario.
7. Confirmación de recepción de eventos en Wazuh.

---

## Configuración

### Wazuh Agent

Se configuró el agente para establecer comunicación con Wazuh Manager y recolectar las fuentes de telemetría definidas para el laboratorio.

### auditd

Se utilizó el servicio de auditoría para registrar eventos relacionados con:

- accesos y cambios sobre archivos;
- modificaciones de permisos;
- actividad de usuarios;
- procesos y ejecuciones cuando las reglas de auditoría configuradas lo permiten.

### Syslog

Se validó la disponibilidad de registros del sistema y su recolección según la configuración del endpoint.

### systemd journal / journalctl

El **systemd journal** actúa como fuente de registros para servicios administrados por systemd. `journalctl` se utilizó como herramienta de consulta y troubleshooting sobre esos registros.

---

## Validación

Se verificó:

- estado del agente;
- comunicación con Wazuh Manager;
- recepción de eventos;
- visualización desde Wazuh Dashboard;
- consistencia de timestamps;
- disponibilidad de registros provenientes de las fuentes configuradas.

---

## Evidencias

Las evidencias documentadas incluyen:

- estado del Wazuh Agent;
- configuración de auditd;
- registros Syslog;
- eventos del systemd journal;
- eventos recibidos por Wazuh;
- capturas o registros del Dashboard;
- validación de conectividad.

---

## Detecciones implementadas

En esta etapa únicamente se valida la disponibilidad y calidad de la telemetría Linux. Las reglas y casos de detección se documentan en laboratorios posteriores.

---

## Mapeo MITRE ATT&CK

La telemetría Linux puede apoyar investigaciones relacionadas con tácticas y técnicas de **Execution**, **Persistence**, **Privilege Escalation**, **Defense Evasion** y **Discovery**. El mapeo específico se realiza únicamente cuando existe una actividad concreta y evidencia que lo justifique.

---

## Aplicación en un entorno empresarial

Las actividades realizadas representan tareas habituales de un **SOC Analyst**, entre ellas:

- supervisión de agentes;
- verificación de fuentes de logs;
- validación de servicios críticos;
- monitoreo de sistemas Linux;
- troubleshooting de telemetría;
- preparación de evidencia para investigaciones.

---

## Competencias desarrolladas

- Administración de Wazuh Agent.
- Configuración de auditd.
- Gestión y análisis de Syslog.
- Consulta de systemd journal mediante `journalctl`.
- Validación de telemetría Linux.
- Troubleshooting de agentes.
- Security Monitoring sobre Linux.

---

## Lecciones aprendidas

- La calidad de una investigación depende de la calidad de la telemetría disponible.
- `journalctl` es una herramienta de consulta; la fuente de eventos es el systemd journal.
- La validación temprana del agente y de los timestamps reduce errores posteriores.
- Las distintas fuentes Linux deben analizarse de forma complementaria.

---

## Referencias

- Ubuntu Documentation.
- Linux auditd Documentation.
- systemd / journalctl Documentation.
- Wazuh Documentation.
- MITRE ATT&CK.
