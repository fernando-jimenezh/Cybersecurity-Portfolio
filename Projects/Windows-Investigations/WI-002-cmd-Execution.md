# WI-002 - cmd Execution

## Resumen

Se investigó la ejecución de **Windows Command Prompt (cmd.exe)** iniciada desde **PowerShell**, con el objetivo de validar la telemetría generada por Sysmon y su posterior procesamiento por Wazuh SIEM.

Durante la investigación se analizaron los eventos de creación de procesos, la relación entre el proceso padre e hijo y la alerta generada por la regla nativa de Wazuh asociada a este comportamiento.

---

# Objetivo

- Validar la generación de telemetría mediante Sysmon.
- Confirmar la recepción de eventos en Wazuh SIEM.
- Analizar la relación entre PowerShell y cmd.exe.
- Verificar la detección mediante reglas nativas de Wazuh.
- Identificar información útil para una investigación SOC.

---

# Entorno

| Componente | Valor |
|------------|-------|
| Sistema Operativo | Windows 11 |
| SIEM | Wazuh 4.14.5 |
| Telemetría | Sysmon |
| Hipervisor | VirtualBox |

---

# Evidencia

## Comando ejecutado

```powershell
cmd.exe
```

## Evento identificado

| Campo | Valor |
|--------|-------|
| Event ID | 1 |
| Evento | Process Create |
| Image | `C:\Windows\System32\cmd.exe` |
| Parent Image | `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe` |
| Parent CommandLine | `powershell` |
| Usuario | `DESKTOP-7CLFI8R\lab` |
| Process ID | 10908 |
| Parent Process ID | 2128 |
| Integrity Level | High |
| Current Directory | `C:\Users\lab\` |

---

# Hallazgos

Durante la investigación se confirmó que:

- Sysmon registró correctamente la creación del proceso `cmd.exe`.
- El proceso fue iniciado desde `powershell.exe`.
- La ejecución fue asociada al usuario `DESKTOP-7CLFI8R\lab`.
- Wazuh recibió correctamente la telemetría enviada por Sysmon.
- La actividad generó una alerta mediante la regla nativa **92004**.

---

# Análisis

La ejecución de `cmd.exe` desde PowerShell es un comportamiento frecuente tanto en actividades administrativas como durante distintas fases de un ataque.

En este caso, la evidencia muestra que PowerShell actuó como proceso padre de `cmd.exe`, permitiendo reconstruir la cadena completa de ejecución mediante la telemetría registrada por Sysmon.

Aunque este comportamiento puede ser completamente legítimo, también es utilizado por herramientas de administración remota, scripts automatizados y actores maliciosos para ejecutar comandos del sistema operativo.

Por este motivo, el contexto de ejecución y la correlación con otros eventos resultan fundamentales antes de determinar si la actividad representa un incidente de seguridad.

---

# Evaluación del Analista

## ¿La actividad es normal?

No es posible determinarlo únicamente con la evidencia disponible.

## Indicadores relevantes

- PowerShell inició un proceso `cmd.exe`.
- Sysmon registró la creación del proceso mediante Event ID 1.
- El proceso fue ejecutado con **High Integrity**.
- La actividad fue detectada por una regla nativa de Wazuh.
- No se observaron evidencias adicionales que indiquen compromiso del sistema.

## Decisión

Como Analista SOC N1, documentaría la evidencia disponible, validaría si la ejecución corresponde a una actividad administrativa autorizada y revisaría eventos relacionados antes de cerrar el caso o escalar la investigación.

---

# MITRE ATT&CK

| Táctica | Técnica |
|----------|----------|
| Execution | T1059.003 - Windows Command Shell |

---

# Regla Wazuh Detectada

| Campo | Valor |
|--------|-------|
| Rule ID | 92004 |
| Nivel | 4 |
| Descripción | Powershell process spawned Windows command shell instance |

La alerta fue generada automáticamente por el ruleset nativo de Wazuh al detectar la ejecución de `cmd.exe` iniciada desde PowerShell.

---

# Conclusiones

La investigación confirmó que Sysmon y Wazuh registran información suficiente para reconstruir la ejecución de `cmd.exe` iniciada desde PowerShell, incluyendo el proceso padre, el proceso hijo, el usuario responsable, el nivel de integridad y la línea de ejecución.

Asimismo, se verificó que Wazuh incorpora la regla nativa **92004**, capaz de detectar este comportamiento sin necesidad de desarrollar reglas personalizadas.

La evidencia obtenida constituye una base sólida para investigaciones posteriores relacionadas con ejecución de comandos, análisis de procesos y actividades de Threat Hunting dentro de un entorno Windows monitoreado por Wazuh.
