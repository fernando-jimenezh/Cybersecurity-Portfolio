# Incident Response

## Objetivo

Aplicar un proceso estructurado de **Incident Response** para analizar, contener, documentar y comprender incidentes de seguridad detectados durante las actividades de monitoreo del laboratorio, utilizando la información recopilada por **Wazuh SIEM** y otras fuentes de telemetría.

---

# Alcance

Este laboratorio documenta el proceso de respuesta ante incidentes dentro del entorno de laboratorio.

Incluye:

- Recepción de alertas.
- Clasificación del incidente.
- Recolección de información.
- Análisis inicial.
- Contención.
- Erradicación.
- Recuperación.
- Documentación de hallazgos.

---

# Arquitectura

```
Endpoint

↓

Wazuh Agent

↓

Wazuh Manager

↓

Alerta

↓

SOC Analyst

↓

Investigación

↓

Incident Response
```

---

# Tecnologías Utilizadas

## SIEM

- Wazuh

## Sistemas Operativos

- Windows 11
- Ubuntu

## Herramientas

- Sysmon
- PowerShell
- Windows Event Logs
- auditd

## Framework

- MITRE ATT&CK

---

# Requisitos

Antes de iniciar una investigación se verificó:

- Disponibilidad de la telemetría.
- Integridad de los eventos.
- Estado operativo del SIEM.
- Acceso al Dashboard.
- Sincronización horaria.

---

# Implementación

El proceso de respuesta contempla las siguientes etapas:

1. Identificación del incidente.
2. Clasificación inicial.
3. Recolección de información.
4. Análisis de los eventos.
5. Contención cuando corresponda.
6. Erradicación de la causa.
7. Recuperación del sistema.
8. Documentación técnica.

---

# Configuración

Las investigaciones utilizan la información recopilada por:

- Wazuh SIEM.
- Windows Event Logs.
- Sysmon.
- auditd.
- Journalctl.

---

# Validación

Cada incidente es validado mediante:

- Correlación de eventos.
- Revisión cronológica.
- Confirmación del origen.
- Verificación de evidencias.
- Clasificación del incidente.

---

# Evidencias

Las investigaciones podrán documentar:

- Alertas.
- Eventos.
- Procesos.
- Usuarios.
- Equipos afectados.
- Línea de tiempo.
- Hallazgos.

---

# Detecciones Implementadas

Las investigaciones utilizan las reglas disponibles en **Wazuh** para apoyar el proceso de análisis.

Las reglas desarrolladas específicamente para cada escenario serán documentadas en **Projects**.

---

# Mapeo MITRE ATT&CK

Cada incidente será relacionado con las tácticas y técnicas correspondientes del framework **MITRE ATT&CK**, facilitando la comprensión del comportamiento observado y la cobertura de las capacidades de detección.

---

# Aplicación en un Entorno Empresarial

Las actividades desarrolladas representan funciones habituales de un **SOC Analyst** durante la gestión de incidentes, incluyendo:

- Análisis de alertas.
- Investigación de eventos.
- Correlación de información.
- Clasificación de incidentes.
- Documentación técnica.
- Comunicación de hallazgos.

---

# Competencias Desarrolladas

Al finalizar este laboratorio se fortalecieron las siguientes competencias:

- Incident Response.
- Análisis de incidentes.
- Correlación de eventos.
- Gestión de evidencias.
- MITRE ATT&CK.
- Documentación técnica.

---

# Lecciones Aprendidas

- La rapidez en la identificación mejora la capacidad de respuesta.
- La correlación de múltiples fuentes proporciona mayor contexto para la investigación.
- La documentación adecuada facilita la mejora continua del proceso de respuesta.
- La calidad de la telemetría influye directamente en la efectividad del análisis.

---

# Referencias

- Wazuh Documentation
- MITRE ATT&CK
- Microsoft Learn
- NIST Computer Security Incident Handling Guide
