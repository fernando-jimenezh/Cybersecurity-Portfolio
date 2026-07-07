# Threat Hunting

## Objetivo

Desarrollar una metodología estructurada para identificar comportamientos anómalos y actividades potencialmente maliciosas mediante el análisis de la telemetría generada por los sistemas del laboratorio, utilizando **Wazuh SIEM** y el framework **MITRE ATT&CK** como base para las investigaciones.

---

# Alcance

Este laboratorio documenta el proceso de **Threat Hunting** realizado sobre los eventos recopilados por el laboratorio.

Incluye:

- Definición de hipótesis.
- Análisis de eventos.
- Correlación de información.
- Validación de actividad.
- Clasificación de hallazgos.
- Documentación técnica.

Las investigaciones específicas serán desarrolladas en los proyectos contenidos dentro de la carpeta **Projects**.

---

# Arquitectura

```
Windows 11          Ubuntu
      │                 │
      ▼                 ▼
 Wazuh Agent      Wazuh Agent
        │             │
        └──────┬──────┘
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
        Threat Hunting
```

---

# Tecnologías Utilizadas

## SIEM

- Wazuh

## Sistemas Operativos

- Windows 11
- Ubuntu

## Frameworks

- MITRE ATT&CK

## Herramientas

- Sysmon
- PowerShell
- Windows Event Logs
- auditd
- Sigma

---

# Requisitos

Antes de realizar actividades de **Threat Hunting** se verificó:

- Recepción de telemetría.
- Funcionamiento del SIEM.
- Estado de los agentes.
- Sincronización de eventos.
- Calidad de los registros recopilados.

---

# Metodología

Las investigaciones siguen una metodología basada en hipótesis.

Proceso utilizado:

1. Definir una hipótesis.
2. Identificar fuentes de información.
3. Consultar eventos.
4. Correlacionar información.
5. Validar resultados.
6. Documentar hallazgos.

---

# Hipótesis de Investigación

Algunos ejemplos de hipótesis que serán desarrolladas durante este laboratorio son:

- Ejecución anómala de **PowerShell**.
- Uso de **LOLBins**.
- Creación de procesos sospechosos.
- Modificaciones del Registro de Windows.
- Persistencia mediante tareas programadas.
- Creación de nuevos usuarios.
- Escalamiento de privilegios.
- Actividad inusual en sistemas Linux.

Cada hipótesis será desarrollada posteriormente mediante casos prácticos.

---

# Fuentes de Información

Las investigaciones utilizan información proveniente de:

## Windows

- Windows Event Logs
- Sysmon
- PowerShell Logging

## Linux

- auditd
- Syslog
- Journalctl

## Wazuh

- Security Events
- Agent Events
- Rule Alerts

---

# Validación

Cada investigación contempla:

- Confirmación del evento.
- Validación del contexto.
- Correlación entre múltiples eventos.
- Identificación del origen.
- Clasificación del resultado.

---

# Evidencias

Las evidencias podrán incluir:

- Eventos registrados.
- Alertas.
- Procesos observados.
- Línea de tiempo.
- Comandos ejecutados.
- Consultas realizadas.
- Hallazgos obtenidos.

---

# Detecciones Implementadas

Durante este laboratorio se utilizan las reglas predeterminadas de **Wazuh** para apoyar las investigaciones.

Las reglas personalizadas serán desarrolladas en el laboratorio **Detection Engineering**.

---

# Mapeo MITRE ATT&CK

Las investigaciones serán relacionadas con las tácticas y técnicas correspondientes del framework **MITRE ATT&CK**.

El objetivo es comprender el comportamiento observado y mejorar las capacidades de detección del laboratorio.

---

# Aplicación en un Entorno Empresarial

Las actividades desarrolladas representan tareas habituales de un **Threat Hunter**, entre ellas:

- Investigación proactiva de amenazas.
- Validación de alertas.
- Correlación de eventos.
- Identificación de comportamientos anómalos.
- Reducción de falsos positivos.
- Generación de hipótesis de investigación.

---

# Competencias Desarrolladas

Al finalizar este laboratorio se fortalecieron las siguientes competencias:

- Threat Hunting.
- Análisis de eventos.
- Correlación de información.
- Investigación basada en hipótesis.
- MITRE ATT&CK.
- Documentación técnica.
- Pensamiento analítico.

---

# Lecciones Aprendidas

- La calidad de una investigación depende de la calidad de la telemetría disponible.
- Formular una hipótesis permite orientar el análisis y reducir el tiempo de investigación.
- La correlación de múltiples fuentes proporciona mayor contexto para comprender una actividad.
- La documentación de los hallazgos facilita la mejora continua de las capacidades de detección.

---

# Referencias

- MITRE ATT&CK
- Wazuh Documentation
- Microsoft Learn
- Sigma Documentation
