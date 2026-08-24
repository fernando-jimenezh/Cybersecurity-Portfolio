# WI-001 — PowerShell EncodedCommand

## Resumen

Se investigó la ejecución de **PowerShell** utilizando el parámetro **`-EncodedCommand`** con el objetivo de validar la telemetría generada por **Sysmon** y su posterior recolección en **Wazuh SIEM**.

Este documento corresponde a la **primera de tres pruebas controladas** realizadas sobre el mismo escenario. Su objetivo principal fue validar la evidencia de proceso y establecer una línea base antes de comprobar la regla nativa de Wazuh y ampliar el análisis mediante Threat Hunting.

## Relación con las tres pruebas

| Prueba | Objetivo | Resultado principal |
|---|---|---|
| **Prueba 1 — Telemetría base** | Ejecutar PowerShell desde `cmd.exe` y verificar Sysmon/Wazuh | Telemetría recibida correctamente; `cmd.exe` quedó registrado como proceso padre |
| **Prueba 2 — Detection Validation** | Ejecutar un PowerShell hijo desde PowerShell usando `-EncodedCommand` | Se cumplió la lógica de la regla nativa **92057** y se generó la alerta |
| **Prueba 3 — Repetibilidad / Threat Hunting** | Repetir la actividad y buscar ejecuciones relacionadas | Se observaron **3 ejecuciones** con `EncodedCommand` en total y **1 alerta 92057** |

La diferencia entre los resultados es esperada: la regla **92057** requiere que el proceso padre sea `powershell.exe`. Por ello, la evidencia de esta primera prueba, cuyo padre es `cmd.exe`, no debe confundirse con el evento específico que activó la regla.

---

## Objetivo

- Validar la generación de telemetría mediante Sysmon.
- Confirmar la recepción del evento en Wazuh SIEM.
- Analizar proceso, línea de comandos, proceso padre, usuario e Integrity Level.
- Establecer una evidencia base para la posterior Detection Validation.

---

## Entorno

| Componente | Valor |
|---|---|
| Sistema operativo | Windows 11 |
| SIEM | Wazuh 4.14.5 |
| Telemetría | Sysmon |
| Hipervisor | VirtualBox |

---

## Evidencia

### Comando ejecutado

```powershell
powershell.exe -EncodedCommand QQA=
```

`QQA=` es una cadena **Base64 válida**. Interpretada con la codificación esperada por Windows PowerShell para `-EncodedCommand` (UTF-16LE), representa el texto `A`. El contenido resultante no constituye por sí solo un comando útil y puede producir un error de ejecución; para este laboratorio lo relevante era generar telemetría controlada sin ejecutar una carga maliciosa.

### Evento identificado

| Campo | Valor |
|---|---|
| Event ID | 1 |
| Evento | Process Create |
| Image | `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe` |
| Parent Image | `C:\Windows\System32\cmd.exe` |
| CommandLine | `powershell.exe -EncodedCommand QQA=` |
| Usuario | `DESKTOP-7CLFI8R\lab` |
| Process ID | 8584 |
| Parent Process ID | 11128 |
| Integrity Level | High |

---

## Hallazgos

Durante esta prueba se confirmó que:

- Sysmon registró correctamente el **Event ID 1 (Process Create)**.
- El parámetro `-EncodedCommand` quedó disponible en el campo `CommandLine`.
- PowerShell fue iniciado desde `cmd.exe`.
- La ejecución quedó asociada al usuario del laboratorio.
- Wazuh recibió correctamente la telemetría.
- Este evento por sí solo **no cumple la condición `parentImage = powershell.exe` de la regla 92057**.

---

## Análisis técnico

El uso de `-EncodedCommand` permite proporcionar a PowerShell instrucciones codificadas en Base64. La codificación no equivale a cifrado y no implica necesariamente actividad maliciosa; puede utilizarse en automatización y administración legítima. Sin embargo, también puede emplearse para **command obfuscation**, por lo que requiere análisis contextual.

La evidencia disponible en esta prueba permite reconstruir la relación:

```text
cmd.exe
   │
   ▼
powershell.exe -EncodedCommand QQA=
   │
   ▼
Sysmon Event ID 1
   │
   ▼
Wazuh
```

---

## Evaluación del analista

La actividad no debe clasificarse automáticamente como maliciosa. Un analista SOC debe revisar, entre otros elementos:

- proceso padre e hijos;
- usuario;
- Integrity Level;
- otras ejecuciones de PowerShell;
- conexiones de red relacionadas;
- actividad posterior;
- reglas o alertas generadas.

La validación específica de la regla **92057** se documenta en **DR-001**.

---

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| Execution | **T1059.001 — PowerShell** |
| Defense Evasion / contexto de ofuscación | **T1027.010 — Command Obfuscation** |

> El mapeo a T1027.010 describe el posible uso de codificación para dificultar el análisis; no implica que esta prueba controlada haya sido maliciosa.

---

## Conclusión

La primera prueba confirmó que Sysmon y Wazuh registran información suficiente para reconstruir una ejecución de PowerShell mediante `-EncodedCommand`, incluyendo proceso, línea de comandos, proceso padre, usuario e Integrity Level.

Esta evidencia constituye la línea base del escenario. La segunda prueba valida la regla nativa Wazuh **92057**, mientras que la tercera amplía el análisis mediante **Threat Hunting** y correlación de las tres ejecuciones.

---

## Proyectos relacionados

- **DR-001** — Validate Wazuh Rule 92057 — PowerShell EncodedCommand.
- **TH-001** — Threat Hunting: PowerShell EncodedCommand.
- **CS-001** — PowerShell EncodedCommand Investigation.
