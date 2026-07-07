# WI-001 - PowerShell EncodedCommand

## Resumen

Se investigó la ejecución de **PowerShell** utilizando el parámetro **-EncodedCommand** con el objetivo de validar la telemetría generada por Sysmon y su posterior recolección en Wazuh SIEM.

Durante la investigación se analizaron los eventos generados por la creación del proceso y las alertas asociadas, evaluando la información disponible para un analista SOC.

---

# Objetivo

- Validar la generación de telemetría mediante Sysmon.
- Confirmar la recepción de eventos en Wazuh SIEM.
- Analizar la información disponible para una investigación.
- Identificar indicadores relevantes para detección.

---

# Entorno

| Componente | Valor |
|------------|-------|
| Sistema Operativo | Windows 11 |
| SIEM | Wazuh |
| Telemetría | Sysmon |
| Hipervisor | VirtualBox |

---

# Evidencia

## Comando ejecutado

```powershell
powershell.exe -EncodedCommand QQA=
```

## Evento identificado

| Campo | Valor |
|--------|-------|
| Event ID | 1 |
| Evento | Process Create |
| Image | `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe` |
| Parent Image | `C:\Windows\System32\cmd.exe` |
| Usuario | `DESKTOP-7CLFI8R\lab` |
| Process ID | 8584 |
| Parent Process ID | 11128 |
| Integrity Level | High |

---

# Hallazgos

Durante la investigación se confirmó que:

- Sysmon registró correctamente la creación del proceso.
- El parámetro **-EncodedCommand** quedó registrado en el campo **CommandLine**.
- PowerShell fue iniciado desde **cmd.exe**.
- La ejecución fue asociada al usuario **DESKTOP-7CLFI8R\lab**.
- La telemetría fue recibida correctamente por Wazuh.

---

# Análisis

El uso del parámetro **-EncodedCommand** constituye un comportamiento que requiere revisión, ya que es utilizado tanto por administradores para automatización como por atacantes para ocultar comandos mediante codificación Base64.

La evidencia disponible no permite clasificar la actividad como maliciosa sin considerar información adicional sobre el contexto de ejecución.

---

# Evaluación del Analista

## ¿La actividad es normal?

No es posible determinarlo únicamente con la evidencia disponible.

## Indicadores relevantes

- Uso de **-EncodedCommand**.
- Ejecución de **PowerShell** desde **cmd.exe**.
- Proceso ejecutado con **High Integrity**.
- Telemetría registrada por Sysmon.

## Decisión

La actividad merece revisión antes de ser descartada.

Como analista SOC N1, recopilaría evidencia adicional y, si el análisis excede mis responsabilidades, escalaría el caso conforme a los procedimientos establecidos por la organización.

---

# MITRE ATT&CK

| Táctica | Técnica |
|----------|----------|
| Execution | T1059.001 - PowerShell |

> **Nota:** Durante la investigación se observó una alerta asociada a la técnica **T1105**. Sin embargo, la evidencia analizada corresponde a la ejecución de PowerShell mediante **-EncodedCommand**, por lo que se considera más representativa la técnica **T1059.001 (PowerShell)**. La clasificación definitiva dependerá del contexto completo de la actividad.

---

# Conclusiones

La investigación confirmó que Sysmon y Wazuh registran información suficiente para reconstruir la ejecución de PowerShell mediante **-EncodedCommand**, incluyendo el proceso ejecutado, la línea de comandos, el proceso padre, el usuario y el nivel de integridad.

Estos elementos proporcionan el contexto necesario para que un analista SOC inicie una investigación y determine si la actividad corresponde a un comportamiento administrativo legítimo o a una posible actividad maliciosa.
