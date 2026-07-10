# CS-002 - Suspicious Command Prompt Investigation

## Executive Summary

During routine monitoring activities, Wazuh generated an alert indicating that **PowerShell** spawned a **Windows Command Prompt (cmd.exe)** process.

Although this parent-child relationship may occur during legitimate administrative activities, it is also commonly associated with attacker tradecraft, making contextual analysis essential.

This case study documents the complete investigation, from telemetry generation through Sysmon to alert correlation within Wazuh, validating the native detection capabilities of Rule **92004**.

---

# Objective

Investigate the execution of **cmd.exe** initiated from **PowerShell**, validate the telemetry collected by Sysmon and analyze the event from the perspective of a SOC analyst.

---

# Scenario

As part of a controlled laboratory exercise, PowerShell was used to launch a Windows Command Prompt session.

Command executed:

```powershell
cmd.exe
```

The objective was to generate controlled telemetry to validate native Wazuh detection and document the complete investigation process.

---

# Scope

The investigation included:

- Telemetry generation on Windows 11.
- Sysmon Process Create event validation.
- Wazuh event collection.
- Native rule validation.
- Parent-child process analysis.
- MITRE ATT&CK mapping.
- SOC investigation.

---

# Investigation

The investigation started after Wazuh generated Rule **92004**, identifying that **PowerShell** launched **cmd.exe**.

Sysmon Event ID 1 provided detailed telemetry describing the new process, including:

- Parent process
- Child process
- Command line
- User
- Integrity level
- Process identifiers

The event was successfully processed by Wazuh and correlated with the native detection rule.

---

# Timeline

| Time | Event |
|------|-------|
| 19:38:32 | PowerShell launched cmd.exe |
| 19:38:32 | Sysmon generated Event ID 1 |
| 19:38:33 | Wazuh received the event |
| 19:38:33 | Rule 92004 generated the alert |
| Afterwards | Technical investigation initiated |
| Final | Case documented |

---

# Evidence

## Observed Event

| Field | Value |
|--------|-------|
| Provider | Microsoft-Windows-Sysmon |
| Event ID | 1 |
| Process | cmd.exe |
| Parent Process | powershell.exe |
| User | DESKTOP-7CLFI8R\lab |
| Integrity Level | High |
| Endpoint | W11-Lab |

---

## Detection

| Field | Value |
|--------|-------|
| Rule ID | 92004 |
| Description | Powershell process spawned Windows command shell instance |
| MITRE | T1059.003 |

---

# Technical Analysis

PowerShell spawning **cmd.exe** is a common administrative behavior.

However, it is also frequently abused by attackers during post-exploitation to execute additional commands using trusted Windows binaries (LOLBins).

The investigation confirmed that:

- The activity originated from the laboratory endpoint.
- The execution was initiated by the laboratory user.
- Only one alert was generated.
- No evidence of persistence was identified.
- No evidence of lateral movement was identified.
- No additional suspicious executions were observed.

The available evidence supports classifying the activity as an expected laboratory simulation.

---

# Detection Validation

The investigation also confirmed the internal processing path followed by Wazuh.

```text
Windows Event

        │

        ▼

Rule 18100

        │

        ▼

Rule 184665

(Sysmon Event 1)

        │

        ▼

Group

sysmon_event1

        │

        ▼

Rule 92004

        │

        ▼

Security Alert
```

The native rule successfully identified the parent-child relationship without requiring any custom detection logic.

---

# MITRE ATT&CK

| Tactic | Technique |
|----------|-----------|
| Execution | T1059.003 – Windows Command Shell |

---

# Risk Assessment

| Factor | Assessment |
|---------|------------|
| Probability | Medium |
| Impact | Medium |
| Priority | Medium |

PowerShell launching cmd.exe should always be reviewed because the same behavior can be observed during both legitimate administration and malicious activity.

---

# Recommendations

- Validate the execution context.
- Review parent-child process relationships.
- Correlate with additional Sysmon events.
- Investigate repeated executions.
- Review associated network activity.
- Expand hunting activities to other LOLBins.

---

# Lessons Learned

- Parent-child process analysis provides valuable context during investigations.
- Native Wazuh rules cover many common execution techniques.
- Rule validation should precede custom Detection Engineering.
- Sysmon provides sufficient telemetry to reconstruct process execution.
- Threat Hunting complements alert triage by identifying related activity across the environment.

---

# References

- WI-002 – cmd Execution
- TH-002 – LOLBins Activity
- DR-002 – Validate Wazuh Rule 92004
- Microsoft Sysmon
- MITRE ATT&CK – T1059.003

---

# Conclusion

This investigation validated the complete detection workflow for **PowerShell spawning Windows Command Prompt**, from telemetry generation through Sysmon to native alert generation within Wazuh.

The analysis confirmed that Rule **92004** provides native coverage for this behavior, while the surrounding investigation demonstrated how SOC analysts can determine whether an alert represents legitimate administration or potentially malicious activity.

The case also reinforces the importance of correlating process relationships, telemetry and detection logic to produce high-quality security investigations.
