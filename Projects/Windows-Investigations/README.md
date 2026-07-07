# Windows Investigations

## Descripción

La carpeta **Windows Investigations** reúne las investigaciones técnicas realizadas sobre eventos de seguridad generados en sistemas **Windows**, utilizando la telemetría recopilada por **Wazuh SIEM**, **Sysmon** y **Windows Event Logs**.

Cada investigación documenta el proceso de análisis aplicado para comprender el comportamiento observado, validar alertas y determinar si una actividad corresponde a una operación legítima o potencialmente maliciosa.

---

# Objetivos

Esta sección tiene como finalidad:

- Analizar eventos de seguridad en sistemas Windows.
- Documentar investigaciones técnicas.
- Comprender el comportamiento de procesos y servicios.
- Validar alertas generadas por el SIEM.
- Correlacionar eventos provenientes de múltiples fuentes.
- Fortalecer las capacidades de análisis e investigación.

---

# Alcance

Las investigaciones podrán incluir escenarios relacionados con:

- PowerShell.
- CMD.
- LOLBins.
- Sysmon.
- Windows Event Logs.
- Servicios del sistema.
- Registro de Windows.
- Persistencia.
- Programación de tareas.
- Autenticación.
- Gestión de usuarios.
- Procesos.
- Conexiones de red.
- Actividad administrativa.

Cada caso será documentado de forma independiente.

---

# Metodología

Todas las investigaciones seguirán una metodología uniforme para garantizar consistencia y facilitar su comprensión.

## Estructura

- Resumen Ejecutivo.
- Objetivo.
- Escenario.
- Fuente de Información.
- Análisis.
- Hallazgos.
- Evaluación.
- Conclusión.
- Mapeo MITRE ATT&CK.
- Competencias Desarrolladas.
- Lecciones Aprendidas.

---

# Fuentes de Información

Las investigaciones podrán utilizar información proveniente de:

- Wazuh Dashboard.
- Wazuh Manager.
- Sysmon.
- Windows Event Logs.
- PowerShell Logging.
- Registros de seguridad.
- Procesos del sistema.
- Información de usuarios.
- Alertas del SIEM.

---

# Tipos de Investigaciones

Algunos ejemplos de investigaciones que formarán parte de esta sección son:

- Ejecución de **cmd.exe** desde **PowerShell**.
- Uso de **PowerShell** para automatización.
- Ejecución de **LOLBins**.
- Creación de procesos sospechosos.
- Persistencia mediante tareas programadas.
- Creación de servicios.
- Cambios en el Registro de Windows.
- Actividad administrativa inusual.
- Escalamiento de privilegios.
- Ejecución de herramientas de administración remota.

Cada investigación será documentada de forma independiente y basada en eventos generados dentro del laboratorio.

---

# Objetivo del Portafolio

Las investigaciones documentadas en esta sección representan la aplicación práctica de los conocimientos adquiridos durante el desarrollo del laboratorio, permitiendo demostrar experiencia en el análisis de eventos, validación de alertas e investigación de incidentes en sistemas Windows.
