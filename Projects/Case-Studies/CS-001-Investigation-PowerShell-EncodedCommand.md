# CS-001 - Investigation of PowerShell EncodedCommand Execution

## Executive Summary

Durante las actividades de monitoreo del laboratorio se identificó la ejecución de **PowerShell** utilizando el parámetro **-EncodedCommand**, una técnica ampliamente utilizada para ejecutar comandos codificados en Base64 y frecuentemente observada durante actividades ofensivas y campañas de malware.

La investigación permitió validar la telemetría generada por Sysmon, confirmar la recepción del evento por Wazuh y verificar que la actividad fue detectada correctamente mediante la regla nativa **92057**, sin requerir reglas personalizadas adicionales.

---

# Objetivo

Investigar la ejecución de PowerShell utilizando **-EncodedCommand**, validar el proceso completo de detección dentro de Wazuh y documentar el análisis técnico realizado durante la investigación.

---

# Escenario

Como parte del laboratorio se ejecutó una prueba controlada utilizando PowerShell para generar telemetría relacionada con comandos codificados.

Comando ejecutado:

```powershell
powershell.exe -EncodedCommand QQA=
```

Aunque el contenido Base64 utilizado es inválido y genera un error durante la ejecución, el objetivo fue producir evidencia suficiente para validar las capacidades de monitoreo y detección del SIEM.

---

# Alcance

La investigación incluyó:

- Generación de telemetría en Windows.
- Registro del evento mediante Sysmon.
- Recepción del evento por Wazuh.
- Validación del procesamiento del evento.
- Revisión del motor de reglas.
- Confirmación de la detección nativa.
- Documentación de los resultados.

---

# Investigation

La investigación comenzó tras identificar la ejecución de PowerShell mediante el parámetro **-EncodedCommand**.

El evento fue registrado por Sysmon como **Event ID 1 (Process Create)**, proporcionando información detallada sobre el proceso ejecutado, la línea de comandos utilizada, el proceso padre y el usuario responsable de la ejecución.

Posteriormente se verificó que el evento fue recibido correctamente por Wazuh, donde fue procesado por el motor de reglas hasta generar una alerta correspondiente a la técnica detectada.

---

# Timeline

| Hora | Evento |
|------|--------|
| 18:09:48 | Ejecución de PowerShell con **-EncodedCommand** |
| 18:09:48 | Sysmon registra Event ID 1 |
| 18:09:56 | Wazuh recibe el evento |
| 18:09:56 | Se activa la regla nativa 92057 |
| Posteriormente | Se inicia la investigación técnica |
| Final | Caso documentado |

---

# Evidence

## Evento observado

| Campo | Valor |
|--------|-------|
| Provider | Microsoft-Windows-Sysmon |
| Event ID | 1 |
| Process | powershell.exe |
| Parent Process | cmd.exe |
| CommandLine | powershell.exe -EncodedCommand QQA= |
| User | lab |
| Source | Sysmon |

---

## Detección

| Campo | Valor |
|--------|-------|
| Rule ID | 92057 |
| Detección | PowerShell Encoded Command |
| Resultado | Detectado correctamente |

---

# Technical Analysis

La ejecución de PowerShell utilizando **-EncodedCommand** constituye una técnica utilizada para ocultar comandos durante su ejecución.

Aunque este comportamiento puede formar parte de actividades administrativas legítimas, también es ampliamente empleado por actores maliciosos para dificultar el análisis y evadir mecanismos básicos de detección.

Durante la investigación se observó que el proceso fue iniciado desde **cmd.exe**, ejecutándose bajo el usuario del laboratorio.

La evidencia disponible no permitió asociar actividad adicional que indicara compromiso del sistema, sin embargo, el comportamiento requiere validación debido a su naturaleza.

---

# Detection Validation

Como parte del análisis se revisó el funcionamiento interno del motor de reglas de Wazuh.

Se verificó la cadena de procesamiento utilizada para eventos Sysmon Event ID 1:

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

La investigación confirmó que Wazuh incorpora una regla nativa capaz de detectar este comportamiento.

No fue necesario desarrollar una regla personalizada.

---

# MITRE ATT&CK

| Táctica | Técnica |
|----------|----------|
| Execution | T1059.001 – PowerShell |

---

# Risk Assessment

| Factor | Evaluación |
|---------|------------|
| Probabilidad | Media |
| Impacto | Medio |
| Prioridad | Media |

La utilización de **-EncodedCommand** requiere análisis contextual, ya que puede corresponder tanto a actividades administrativas como a técnicas empleadas por atacantes.

---

# Recommendations

- Validar el contexto de ejecución.
- Identificar el usuario responsable.
- Revisar procesos padre e hijos.
- Correlacionar con eventos Sysmon adicionales.
- Verificar conexiones de red asociadas.
- Buscar ejecuciones similares dentro del entorno.
- Revisar actividad posterior del proceso.

---

# Lessons Learned

- Una única acción puede generar múltiples fuentes de telemetría.
- Sysmon proporciona información detallada para investigaciones de procesos.
- Antes de desarrollar reglas personalizadas es recomendable validar las capacidades nativas del SIEM.
- Comprender el flujo interno del motor de reglas facilita el proceso de Detection Engineering.
- La correlación entre evidencia, reglas y telemetría mejora significativamente la calidad del análisis.

---

# Referencias

- WI-001 – PowerShell EncodedCommand Investigation
- DR-001 – Validate Wazuh Rule 92057
- Microsoft Sysmon
- MITRE ATT&CK – T1059.001

---

# Conclusion

La investigación permitió validar exitosamente el flujo completo de detección de PowerShell utilizando **-EncodedCommand**.

La evidencia generada en el laboratorio confirmó el correcto funcionamiento de Sysmon como fuente de telemetría y de Wazuh como plataforma de monitoreo y detección.

Asimismo, el análisis permitió verificar que la regla nativa **92057** proporciona cobertura para esta técnica, demostrando la importancia de revisar y validar el contenido existente antes de desarrollar reglas personalizadas.

Este caso de estudio permitió fortalecer conocimientos relacionados con monitoreo de seguridad, investigación de eventos, análisis de telemetría, Detection Engineering y validación de capacidades de detección dentro de un entorno Blue Team.
