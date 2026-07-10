# TH-001 - Threat Hunting: PowerShell EncodedCommand

## Executive Summary

Durante las actividades de Threat Hunting se investigó la ejecución de **PowerShell** utilizando el parámetro **-EncodedCommand**, una técnica frecuentemente utilizada para ocultar comandos mediante codificación Base64.

El objetivo fue determinar si la alerta observada correspondía a una actividad aislada o formaba parte de una secuencia más amplia de actividad maliciosa dentro del entorno monitoreado.

La investigación confirmó que la actividad estuvo limitada al laboratorio y no se identificaron indicadores adicionales de compromiso.

---

# Objective

Validate whether the execution of PowerShell using the `-EncodedCommand` parameter corresponds to an isolated event or represents a broader malicious activity within the monitored environment.

---

# Hunting Hypothesis

PowerShell executed with the `-EncodedCommand` parameter is frequently associated with defense evasion, payload obfuscation and malicious script execution.

Hypothesis:

> If an attacker executed an encoded PowerShell command, additional executions or related indicators should also exist within the environment.

---

# Environment

| Component | Value |
|-----------|-------|
| Operating System | Windows 11 |
| SIEM | Wazuh 4.14.5 |
| Telemetry | Sysmon |
| Hypervisor | VirtualBox |

---

# Investigation Methodology

The investigation expanded from the original alert to determine:

- Number of EncodedCommand executions.
- Total PowerShell activity.
- Detection rules triggered.
- Affected endpoints.
- Users involved.
- Related process activity.

---

# Hunting Queries

## Encoded PowerShell Executions

```kql
data.win.eventdata.commandLine:*EncodedCommand*
```

**Result**

- 3 events identified.

---

## All PowerShell Executions

```kql
data.win.eventdata.image:*powershell.exe*
```

**Result**

- 10 PowerShell executions observed.

---

## Detection Rule

```kql
rule.id:92057
```

**Result**

- 1 alert generated.

---

## Affected Endpoint

```kql
agent.name:W11-Lab
```

**Result**

- Activity limited to the laboratory endpoint.

---

## User

```kql
data.win.eventdata.user:*
```

**Result**

Primary observed user:

```
DESKTOP-7CLFI8R\lab
```

---

# Findings

The investigation determined:

- Three PowerShell executions contained the **-EncodedCommand** parameter.
- Only one execution generated the detection rule.
- No additional hosts were affected.
- No evidence of lateral movement was identified.
- No persistence mechanisms were observed.
- The activity remained isolated within the laboratory environment.

---

# Indicators Reviewed

## Process

```
powershell.exe
```

## Command Line

```
powershell.exe -EncodedCommand QQA=
```

## Parent Process

```
cmd.exe
```

## User

```
DESKTOP-7CLFI8R\lab
```

## Endpoint

```
W11-Lab
```

---

# Threat Hunting Assessment

The investigation did not identify evidence suggesting an active compromise.

The encoded PowerShell execution corresponded to a controlled laboratory simulation used to validate detection capabilities.

Although the use of **-EncodedCommand** is frequently associated with malicious activity, the available evidence indicated that the execution was expected and limited to the laboratory environment.

No additional suspicious PowerShell activity was identified during the investigation period.

---

# MITRE ATT&CK

| Tactic | Technique |
|----------|-----------|
| Execution | T1059.001 – PowerShell |
| Defense Evasion | T1027 – Obfuscated Files or Information |

---

# Recommendations

- Continue monitoring PowerShell executions using **-EncodedCommand**.
- Correlate PowerShell activity with parent and child processes.
- Review Script Block Logging events when available.
- Correlate with network connections and subsequent process activity.
- Maintain detection rules for PowerShell abuse.

---

# Lessons Learned

- PowerShell is frequently used for legitimate administrative tasks.
- The **-EncodedCommand** parameter should always receive additional investigation.
- Threat Hunting provides the context necessary to determine whether an alert is isolated or part of a broader attack.
- Correlating Sysmon telemetry with Wazuh detections significantly improves investigation quality.

---

# Conclusion

The Threat Hunting activity confirmed that the detected execution corresponded to a controlled laboratory simulation.

No additional indicators of compromise were identified, allowing the activity to be classified as an isolated event generated for detection validation purposes.

The investigation demonstrated the effectiveness of Sysmon telemetry and Wazuh correlation capabilities for identifying and contextualizing encoded PowerShell executions.

---

# References

- Microsoft Sysmon
- Wazuh Documentation
- MITRE ATT&CK – T1059.001 (PowerShell)
- MITRE ATT&CK – T1027 (Obfuscated Files or Information)

---

# Related Projects

- WI-001 – PowerShell EncodedCommand
- DR-001 – Validate Wazuh Rule 92057
- CS-001 – Investigation PowerShell EncodedCommand
