# Threat Hunting Reports

## Descripción

La carpeta **Threat Hunting Reports** reúne los reportes técnicos generados durante las actividades de **Threat Hunting** realizadas dentro del laboratorio de ciberseguridad.

Cada reporte documenta el proceso de investigación seguido para validar una hipótesis, analizar la información recopilada por **Wazuh SIEM** y determinar la existencia o ausencia de comportamientos potencialmente maliciosos.

El objetivo es demostrar una metodología de investigación estructurada, apoyada en el análisis de telemetría y el framework **MITRE ATT&CK**.

---

# Objetivos

Esta sección tiene como finalidad:

- Documentar ejercicios de Threat Hunting.
- Formular hipótesis de investigación.
- Analizar eventos de seguridad.
- Correlacionar información proveniente de diferentes fuentes.
- Validar hallazgos.
- Documentar los resultados obtenidos.

---

# Alcance

Los reportes podrán estar relacionados con actividades como:

- Ejecución de PowerShell.
- Uso de LOLBins.
- Creación de procesos.
- Persistencia.
- Escalamiento de privilegios.
- Credential Access.
- Defense Evasion.
- Actividad administrativa inusual.
- Cambios en servicios del sistema.
- Eventos de autenticación.

Cada reporte será desarrollado de forma independiente.

---

# Metodología

Todos los reportes seguirán una metodología uniforme para garantizar consistencia y facilitar su comprensión.

## Estructura

- Resumen Ejecutivo.
- Hipótesis de Investigación.
- Objetivo.
- Escenario.
- Fuentes de Información.
- Metodología.
- Análisis.
- Hallazgos.
- Conclusión.
- Mapeo MITRE ATT&CK.
- Competencias Desarrolladas.
- Lecciones Aprendidas.

---

# Fuentes de Información

Los reportes podrán utilizar información proveniente de:

- Wazuh Dashboard.
- Wazuh Manager.
- Sysmon.
- Windows Event Logs.
- auditd.
- Syslog.
- Journalctl.
- Alertas del SIEM.
- Registros del sistema operativo.

---

# Tipos de Reportes

Algunos ejemplos de ejercicios que formarán parte de esta sección son:

- Investigación de actividad inusual en PowerShell.
- Búsqueda de ejecución de LOLBins.
- Identificación de intentos de persistencia.
- Detección de procesos anómalos.
- Investigación de autenticaciones sospechosas.
- Validación de reglas de detección.
- Correlación de eventos entre múltiples equipos.

Cada reporte será documentado de forma independiente y basado en eventos generados dentro del laboratorio.

---

# Objetivo del Portafolio

Los reportes documentados en esta sección representan la aplicación práctica de metodologías de Threat Hunting sobre escenarios reales o simulados, permitiendo demostrar capacidades de investigación, análisis y documentación técnica dentro de un entorno Blue Team.
