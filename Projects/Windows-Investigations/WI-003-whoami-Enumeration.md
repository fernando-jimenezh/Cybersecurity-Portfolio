# WI-003 - whoami Enumeration

## Executive Summary

Durante las actividades de monitoreo del laboratorio se investigó la ejecución del comando **whoami**, una utilidad nativa de Windows utilizada para identificar el usuario bajo el cual se está ejecutando una sesión.

Aunque se trata de una herramienta legítima de administración, también es ampliamente utilizada durante las primeras etapas de reconocimiento por atacantes para obtener información del contexto de ejecución antes de continuar con actividades posteriores.

La investigación permitió validar la telemetría generada por Sysmon, confirmar la recepción del evento en Wazuh y analizar la relación padre-hijo entre los procesos involucrados.

---

# Objective

Investigar la ejecución del comando **whoami**, validar la telemetría generada por Sysmon y analizar la información disponible para un analista SOC durante una investigación inicial.

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

Como parte de una prueba controlada del laboratorio se ejecutó el comando:

```cmd
whoami
```

El objetivo fue generar evidencia que permitiera validar el registro del proceso y analizar la información disponible para una investigación de seguridad.

---

# Evidence

## Executed Command

```cmd
whoami
```

## Process Information

| Field | Value |
|--------|-------|
| Event ID | 1 |
| Event | Process Create |
| Image | C:\Windows\System32\whoami.exe |
| Original File Name | whoami.exe |
| CommandLine | whoami |
| Parent Image | C:\Windows\System32\cmd.exe |
| Parent CommandLine | cmd.exe |
| User | DESKTOP-7CLFI8R\lab |
| Integrity Level | High |
| Process ID | 3004 |
| Parent Process ID | 1672 |

---

# Technical Analysis

Sysmon registró correctamente la creación del proceso **whoami.exe** mediante el **Event ID 1 (Process Create)**.

El evento permitió identificar:

- Proceso ejecutado.
- Línea de comandos.
- Usuario responsable.
- Nivel de integridad.
- Directorio de ejecución.
- Hashes del ejecutable.
- Relación padre-hijo entre procesos.

La evidencia confirmó que **whoami.exe** fue iniciado desde **cmd.exe**, el cual había sido ejecutado previamente durante la prueba del laboratorio.

La cadena completa de procesos observada fue:

```text
PowerShell
      │
      ▼
cmd.exe
      │
      ▼
whoami.exe
```

Este tipo de análisis permite reconstruir la secuencia completa de ejecución durante una investigación.

---

# SOC Analyst Assessment

## Is this activity malicious?

No necesariamente.

El comando **whoami** es utilizado frecuentemente por administradores para verificar el contexto de ejecución.

Sin embargo, también es una de las primeras herramientas utilizadas durante la fase de reconocimiento de un atacante.

## Relevant Indicators

- Ejecución de whoami.exe.
- Parent Process: cmd.exe.
- Usuario ejecutor identificado.
- Integridad High.
- Telemetría registrada por Sysmon.

## Analyst Decision

Como Analista SOC N1, la actividad no debe clasificarse automáticamente como maliciosa.

La decisión correcta consiste en validar el contexto de ejecución y correlacionar el evento con otras actividades del mismo usuario o endpoint antes de cerrar el caso.

---

# MITRE ATT&CK

| Tactic | Technique |
|----------|-----------|
| Discovery | T1033 - System Owner/User Discovery |

---

# Lessons Learned

- Sysmon registra completamente la ejecución de herramientas nativas de Windows.
- La relación Parent-Child Process aporta contexto fundamental durante una investigación.
- Herramientas administrativas legítimas también pueden utilizarse durante actividades ofensivas.
- La correlación de procesos permite reconstruir la línea temporal de ejecución.

---

# Conclusions

La investigación confirmó que Sysmon y Wazuh registran información suficiente para reconstruir la ejecución del comando **whoami**.

Aunque el comando es completamente legítimo, su utilización puede representar una actividad de reconocimiento dependiendo del contexto operacional.

La evidencia obtenida constituye una base sólida para futuras investigaciones relacionadas con Discovery y Threat Hunting.

---

# References

- Microsoft Sysmon
- MITRE ATT&CK – T1033

---

# Related Projects

- TH-003 – Windows Discovery Commands
- DR-003 – Detect whoami Enumeration
- CS-003 – Windows Discovery Investigation
- WI-002 – cmd Execution
