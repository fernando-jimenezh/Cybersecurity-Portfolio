# DR-002 - Validate Wazuh Rule 92004 - cmd Execution

## Objetivo

Validar el funcionamiento de la regla nativa **92004** de Wazuh para detectar la ejecución de **Windows Command Prompt (cmd.exe)** iniciada desde **PowerShell**, verificando la generación de telemetría, el procesamiento del evento y la activación de la detección.

---

# Escenario

Durante la investigación realizada en el laboratorio (WI-002), se inició una instancia de **cmd.exe** desde **PowerShell** para generar telemetría controlada y validar las capacidades de detección del SIEM.

Comando ejecutado:

```powershell
cmd.exe
```

La ejecución fue realizada en un entorno de laboratorio con el objetivo de analizar el flujo completo de procesamiento del evento dentro de Wazuh.

---

# Objetivo de la Validación

Confirmar que:

- Sysmon registra correctamente el evento.
- Wazuh recibe la telemetría.
- El motor de reglas procesa el evento.
- Existe una regla nativa para detectar este comportamiento.
- No es necesario desarrollar una regla personalizada.

---

# Arquitectura

```
Windows 11
      │
      ▼
Sysmon
      │
      ▼
Wazuh Agent
      │
      ▼
Wazuh Manager
      │
      ▼
Rules Engine
      │
      ▼
Rule 92004
      │
      ▼
Alert
```

---

# Tecnologías Utilizadas

- Wazuh 4.14.5
- Windows 11
- Sysmon
- PowerShell
- Windows Command Prompt
- Wazuh Dashboard

---

# Evidencia Analizada

Durante la validación se identificó el siguiente evento:

| Campo | Valor |
|--------|-------|
| Provider | Microsoft-Windows-Sysmon |
| Event ID | 1 |
| Image | `C:\Windows\System32\cmd.exe` |
| Parent Image | `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe` |
| Parent CommandLine | `powershell` |
| User | `DESKTOP-7CLFI8R\lab` |

El evento fue recibido correctamente por Wazuh y generó una alerta mediante la regla nativa **92004**.

---

# Investigación del Motor de Reglas

Como parte de la validación se revisó el ruleset oficial de Wazuh.

Se confirmó la ubicación de la regla:

```
/var/ossec/ruleset/rules/0800-sysmon_id_1.xml
```

También se verificó que la regla utiliza el grupo:

```
sysmon_event1
```

La investigación permitió identificar la siguiente cadena de procesamiento:

```
Windows Event

        │
        ▼

Rule 18100

        │
        ▼

Rule 184665

(Sysmon Event ID 1)

        │
        ▼

Group

sysmon_event1

        │
        ▼

0800-sysmon_id_1.xml

        │
        ▼

Rule 92004
```

Durante la investigación también se revisaron los siguientes archivos del ruleset oficial:

- 0220-msauth_rules.xml
- 0330-sysmon_rules.xml
- 0800-sysmon_id_1.xml

Esto permitió comprender cómo Wazuh clasifica inicialmente los eventos de Windows y posteriormente aplica reglas específicas para Sysmon Event ID 1.

---

# Regla Detectada

**Rule ID**

```
92004
```

**Descripción**

```
Powershell process spawned Windows command shell instance
```

**MITRE ATT&CK**

```
Execution

T1059.003

Windows Command Shell
```

La regla fue activada automáticamente al detectar la creación de un proceso **cmd.exe** iniciado desde **PowerShell**.

---

# Resultado

La investigación permitió validar que:

- Sysmon registró correctamente el Event ID 1.
- Wazuh recibió la telemetría.
- El motor de reglas clasificó correctamente el evento.
- La regla nativa 92004 detectó exitosamente el comportamiento.

No fue necesario desarrollar una regla personalizada.

---

# Análisis

Este laboratorio demuestra la importancia de validar las capacidades nativas del SIEM antes de crear nuevas reglas.

La revisión del ruleset confirmó que Wazuh incorpora una detección específica para la ejecución de **cmd.exe** iniciada desde **PowerShell**, proporcionando cobertura para este comportamiento mediante la regla oficial 92004.

Asimismo, la investigación permitió comprender el flujo interno del motor de reglas y la utilización del grupo **sysmon_event1** como mecanismo de clasificación previo a las reglas de detección.

---

# Lecciones Aprendidas

- Antes de desarrollar reglas personalizadas es recomendable revisar el ruleset oficial.
- Sysmon proporciona información suficiente para detectar relaciones entre procesos.
- El grupo **sysmon_event1** actúa como punto de clasificación para eventos Sysmon Event ID 1.
- Comprender la cadena de procesamiento facilita el trabajo de Detection Engineering.
- Wazuh incorpora múltiples reglas nativas para técnicas comunes de ejecución en Windows.

---

# MITRE ATT&CK

| Táctica | Técnica |
|----------|----------|
| Execution | T1059.003 - Windows Command Shell |

---

# Conclusión

La validación confirmó que Wazuh proporciona cobertura nativa para detectar la ejecución de **Windows Command Prompt** iniciada desde **PowerShell** mediante la regla **92004**.

El laboratorio permitió comprender el flujo completo del evento, desde la generación de la telemetría en Sysmon hasta la activación de la regla oficial dentro del motor de correlación de Wazuh, fortaleciendo conocimientos relacionados con Detection Engineering, análisis del ruleset y validación de capacidades de detección.
