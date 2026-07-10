# CS-001 - Investigation of PowerShell EncodedCommand Execution

## Executive Summary

Durante las actividades de monitoreo del laboratorio se identificó la ejecución de **PowerShell** utilizando el parámetro **-EncodedCommand**, una técnica ampliamente utilizada para ejecutar comandos codificados en Base64 y frecuentemente observada durante actividades ofensivas y campañas de malware.

La investigación permitió validar la telemetría generada por Sysmon, confirmar la recepción del evento por Wazuh y verificar que la actividad fue detectada correctamente mediante la regla nativa **92057**, sin requerir reglas personalizadas adicionales.

El caso permitió reconstruir el flujo completo del evento, desde la creación del proceso hasta la generación de la alerta, proporcionando una visión integral del proceso de investigación dentro de un entorno Blue Team.

---

# Objective

Investigar la ejecución de PowerShell utilizando **-EncodedCommand**, validar el proceso completo de detección dentro de Wazuh y documentar el análisis técnico realizado durante la investigación.

---

# Environment

| Component | Value |
|-----------|-------|
| Operating System | Windows 11 |
| SIEM | Wazuh 4.14.5 |
| Telemetry | Sysmon |
| Hypervisor | VirtualBox |

---

# Scenario

Como parte del laboratorio se ejecutó una prueba controlada utilizando PowerShell para generar telemetría relacionada con comandos codificados.

Comando ejecutado:

```powershell
powershell.exe -EncodedCommand QQA=
```

Aunque el contenido Base64 utilizado es inválido y genera un error durante la ejecución, el objetivo fue producir evidencia suficiente para validar las capacidades de monitoreo y detección del SIEM.

---

# Scope

La investigación incluyó:

- Generación de telemetría en Windows.
- Registro del evento mediante Sysmon.
- Recepción del evento por Wazuh.
- Validación del procesamiento del evento.
- Revisión del motor de reglas.
- Confirmación de la detección nativa.
- Correlación de evidencia.
- Documentación del caso.

---

# Investigation

La investigación comenzó tras identificar la ejecución de PowerShell mediante el parámetro **-EncodedCommand**.

El evento fue registrado por Sysmon como **Event ID 1 (Process Create)**, proporcionando información detallada sobre el proceso ejecutado, la línea de comandos utilizada, el proceso padre y el usuario responsable de la ejecución.

Posteriormente se verificó que el evento fue recibido correctamente por Wazuh, donde fue procesado por el motor de reglas hasta generar la alerta correspondiente.

Finalmente se revisó el ruleset oficial para comprender el flujo interno de procesamiento utilizado por Wazuh antes de generar la detección.

---

# Timeline

| Time | Event |
|------|-------|
| 18:09:48 | PowerShell executed with **-EncodedCommand** |
| 18:09:48 | Sysmon registered Event ID 1 |
| 18:09:56 | Wazuh received the event |
| 18:09:56 | Native Rule 92057 triggered |
| Afterwards | Technical investigation initiated |
| Final | Case documented |

---

# Evidence

## Process Execution

| Field | Value |
|--------|-------|
| Provider | Microsoft-Windows-Sysmon |
| Event ID | 1 |
| Image | powershell.exe |
| Parent Image | cmd.exe |
| Command Line | powershell.exe -EncodedCommand QQA= |
| User | DESKTOP-7CLFI8R\lab |
| Source | Sysmon |

---

## Detection

| Field | Value |
|--------|-------|
| Rule ID | 92057 |
| Description | PowerShell Encoded Command |
| Result | Successfully Detected |

---

# Technical Analysis

La utilización de **-EncodedCommand** constituye una técnica utilizada para ocultar comandos mediante codificación Base64.

Aunque este comportamiento puede formar parte de tareas administrativas legítimas, también es ampliamente empleado por atacantes para dificultar el análisis y evadir mecanismos básicos de detección.

Durante la investigación se confirmó que:

- PowerShell fue iniciado desde **cmd.exe**.
- El proceso fue ejecutado con privilegios elevados (**High Integrity**).
- Sysmon registró toda la información necesaria para reconstruir la ejecución.
- Wazuh correlacionó correctamente el evento y generó la alerta correspondiente.

No se identificó evidencia adicional que indicara compromiso del sistema.

---

# Detection Validation

Como parte del análisis se revisó el funcionamiento interno del motor de reglas de Wazuh.

Se confirmó la siguiente cadena de procesamiento:

```
Windows
        │
        ▼
Sysmon Event ID 1
        │
        ▼
Rule 18100
        │
        ▼
Rule 184665
        │
        ▼
Group sysmon_event1
        │
        ▼
Rule 92057
```

La investigación confirmó que Wazuh incorpora una regla nativa capaz de detectar este comportamiento sin requerir reglas personalizadas.

---

# Risk Assessment

| Factor | Assessment |
|---------|------------|
| Probability | Medium |
| Impact | Medium |
| Priority | Medium |

La utilización de **-EncodedCommand** requiere análisis contextual, ya que puede corresponder tanto a actividades administrativas como a técnicas empleadas por actores maliciosos.

---

# MITRE ATT&CK

| Tactic | Technique |
|----------|-----------|
| Execution | T1059.001 – PowerShell |

---

# Recommendations

- Validar el contexto de ejecución.
- Identificar el usuario responsable.
- Revisar procesos padre e hijos.
- Correlacionar con eventos Sysmon adicionales.
- Revisar conexiones de red asociadas.
- Buscar ejecuciones similares dentro del entorno.
- Analizar actividad posterior del proceso.

---

# Lessons Learned

- Una única acción puede generar múltiples fuentes de telemetría.
- Sysmon proporciona información suficiente para reconstruir la ejecución de procesos.
- Antes de desarrollar reglas personalizadas es recomendable validar el contenido nativo del SIEM.
- Comprender el flujo interno del motor de reglas facilita el trabajo de Detection Engineering.
- La correlación entre evidencia, reglas y telemetría mejora significativamente la calidad de una investigación.

---

# Conclusion

La investigación permitió validar exitosamente el flujo completo de detección de PowerShell utilizando **-EncodedCommand**.

La evidencia generada en el laboratorio confirmó el correcto funcionamiento de Sysmon como fuente de telemetría y de Wazuh como plataforma de monitoreo y detección.

Asimismo, el análisis permitió verificar que la regla nativa **92057** proporciona cobertura para esta técnica, demostrando la importancia de revisar y validar el contenido existente antes de desarrollar reglas personalizadas.

Este caso de estudio fortaleció conocimientos relacionados con monitoreo de seguridad, investigación de eventos, análisis de telemetría, Detection Engineering y validación de capacidades de detección dentro de un entorno Blue Team.

---

# References

- Microsoft Sysmon
- Wazuh Documentation
- MITRE ATT&CK – T1059.001 (PowerShell)

---

# Related Projects

- WI-001 – PowerShell EncodedCommand
- DR-001 – Validate Wazuh Rule 92057
- TH-001 – Threat Hunting: PowerShell EncodedCommand
