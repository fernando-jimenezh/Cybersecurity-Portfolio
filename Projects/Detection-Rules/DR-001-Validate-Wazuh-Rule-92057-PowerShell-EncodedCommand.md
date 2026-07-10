# DR-001 - Validate Wazuh Rule 92057 - PowerShell EncodedCommand

## Executive Summary

This project validates the native **Wazuh Rule 92057**, responsible for detecting PowerShell executions using the **-EncodedCommand** parameter.

The objective was to confirm the complete detection workflow, from Sysmon telemetry generation to Wazuh alert creation, and verify that native detection capabilities already provide coverage for this technique without requiring a custom detection rule.

---

# Objective

Validate the native **Rule 92057** by confirming that:

- Sysmon records the process creation event.
- Wazuh receives the telemetry.
- The event is processed by the rule engine.
- Rule **92057** is triggered correctly.
- No custom detection rule is required.

---

# Scenario

As part of the laboratory investigation, a controlled PowerShell execution was performed using the **-EncodedCommand** parameter.

Command executed:

```powershell
powershell.exe -EncodedCommand QQA=
```

Although the supplied Base64 string is intentionally invalid and generates an execution error, the command successfully produces the telemetry required to validate the detection.

---

# Detection Goal

Validate that Wazuh detects PowerShell executions using the **-EncodedCommand** parameter through its native detection content.

---

# Architecture

```text
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
Rule 92057
      │
      ▼
Security Alert
```

---

# Technologies Used

- Wazuh 4.14.5
- Windows 11
- Sysmon
- PowerShell
- Wazuh Dashboard

---

# Evidence Analyzed

During the validation, the following event was identified:

| Field | Value |
|--------|-------|
| Provider | Microsoft-Windows-Sysmon |
| Event ID | 1 |
| Image | powershell.exe |
| Parent Image | cmd.exe |
| CommandLine | powershell.exe -EncodedCommand QQA= |

The event was successfully collected by the Wazuh Agent and processed by the Wazuh Rules Engine.

---

# Rule Processing Chain

The investigation confirmed the processing chain followed by Wazuh before generating the alert.

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
Rule 92057
        │
        ▼
Alert Generated
```

This processing sequence demonstrates how Wazuh first classifies Sysmon Process Create events before evaluating detection-specific rules.

---

# Rule Definition

The native detection is implemented in the official Wazuh ruleset.

**Rule File**

```text
/var/ossec/ruleset/rules/0800-sysmon_id_1.xml
```

Relevant rule definition:

```xml
<rule id="92057" level="5">
    <if_group>sysmon_event1</if_group>
    <field name="win.eventdata.parentImage" type="pcre2">(?i)\\powershell\.exe</field>
    <field name="win.eventdata.commandLine" type="pcre2">(?i)-encodedcommand</field>
    <description>
        Powershell.exe spawned a powershell process which executed a base64 encoded command
    </description>
    <mitre>
        <id>T1059.001</id>
    </mitre>
</rule>
```

The rule evaluates Sysmon Process Create events and detects PowerShell executions that use the **-EncodedCommand** parameter, a technique commonly associated with command obfuscation and malicious script execution.

---

# Rule Logic

The detection is evaluated only after the event has been classified as a **Sysmon Process Create (Event ID 1)**.

Detection workflow:

```text
Sysmon Event ID 1
        │
        ▼
Group sysmon_event1
        │
        ▼
Parent Process = powershell.exe
        │
        ▼
CommandLine contains -EncodedCommand
        │
        ▼
Rule 92057
        │
        ▼
Alert Generated
```

The rule correlates two primary conditions:

- Parent process must be **powershell.exe**.
- Command line must contain **-EncodedCommand**.

When both conditions are satisfied, Rule **92057** generates the corresponding alert.

This validation confirms that native Wazuh detection already provides coverage for this technique without requiring a custom detection rule.

---

# Detection Validation

The investigation confirmed that:

- Sysmon successfully recorded Event ID 1.
- Wazuh collected the telemetry.
- The Rules Engine processed the event correctly.
- Native Rule **92057** generated the expected alert.
- No custom detection rule was required.

---

# Technical Analysis

Before developing custom detection content, security analysts should always verify whether native SIEM capabilities already provide adequate coverage.

This validation demonstrated that Wazuh includes built-in detection logic for PowerShell executions using **-EncodedCommand**, eliminating the need to duplicate existing functionality.

Understanding the internal processing chain also provides valuable insight into how Sysmon events are classified before reaching detection-specific rules.

---

# MITRE ATT&CK

| Tactic | Technique |
|----------|-----------|
| Execution | T1059.001 – PowerShell |

---

# Lessons Learned

- Native SIEM content should always be reviewed before creating custom rules.
- Sysmon provides high-quality telemetry for process creation events.
- Understanding the internal rule processing chain simplifies Detection Engineering activities.
- Rule validation is an essential step before implementing new detections.
- Understanding the internal rule logic improves detection validation and facilitates future Detection Engineering tasks.

---

# Conclusion

The validation confirmed that Wazuh provides native coverage for detecting PowerShell executions using the **-EncodedCommand** parameter.

The laboratory successfully demonstrated the complete detection workflow, from telemetry generation to alert creation, reinforcing knowledge of Sysmon telemetry, Wazuh rule processing and native detection validation.

This project also highlights the importance of understanding existing SIEM capabilities before developing custom detection content.

---

# Related Projects

- WI-001 – PowerShell EncodedCommand
- TH-001 – PowerShell EncodedCommand
- CS-001 – Investigation of PowerShell EncodedCommand
