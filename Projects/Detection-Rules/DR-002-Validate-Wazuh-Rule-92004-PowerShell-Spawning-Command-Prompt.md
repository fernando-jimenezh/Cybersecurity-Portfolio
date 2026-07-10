# DR-002 - Validate Wazuh Rule 92004 - PowerShell Spawning Command Prompt

## Executive Summary

This project validates the native **Wazuh Rule 92004**, responsible for detecting **cmd.exe** executions initiated by **PowerShell**.

The objective was to confirm the complete detection workflow, from Sysmon telemetry generation to Wazuh alert creation, and verify that native detection capabilities already provide coverage for this behavior without requiring a custom detection rule.

---

# Objective

Validate the native **Rule 92004** by confirming that:

- Sysmon records the process creation event.
- Wazuh receives the telemetry.
- The Rules Engine processes the event correctly.
- Rule **92004** generates the expected alert.
- No custom detection rule is required.

---

# Scenario

As part of the laboratory investigation, a PowerShell session was used to launch **cmd.exe**.

This parent-child relationship generated the required telemetry to validate the native detection.

Observed process chain:

```text
powershell.exe
        │
        ▼
cmd.exe
```

---

# Detection Goal

Validate that Wazuh detects Windows Command Prompt executions launched from PowerShell using its native detection content.

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
Rule 92004
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
- Command Prompt
- Wazuh Dashboard

---

# Evidence Analyzed

The following Sysmon event was analyzed.

| Field | Value |
|--------|-------|
| Event ID | 1 |
| Parent Process | powershell.exe |
| Child Process | cmd.exe |
| Rule ID | 92004 |
| Rule Level | 4 |
| Endpoint | W11-Lab |
| User | DESKTOP-7CLFI8R\lab |

The event was successfully collected and processed by Wazuh.

---

# Rule Processing Chain

The investigation confirmed the following processing sequence inside the Wazuh Rules Engine.

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
Alert Generated
```

This processing chain confirms that the alert is evaluated only after the event has been classified as a Sysmon Process Create event.

---

# Rule Definition

The native detection is implemented in the official Wazuh ruleset.

**Rule File**

```text
/var/ossec/ruleset/rules/0800-sysmon_id_1.xml
```

Relevant rule definition:

```xml
<rule id="92004" level="4">
    <if_group>sysmon_event1</if_group>
    <field name="win.eventdata.commandLine" type="pcre2">\\cmd\.exe</field>
    <field name="win.eventdata.parentImage" type="pcre2">(?i)\\powershell\.exe</field>
    <description>
        Powershell process spawned Windows command shell instance
    </description>
    <mitre>
        <id>T1059.003</id>
    </mitre>
</rule>
```

The rule evaluates Sysmon Process Create events and detects command shell executions launched directly from PowerShell.

---

# Rule Logic

The detection is evaluated only after the event has been classified as **Sysmon Event ID 1**.

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
Child Process = cmd.exe
        │
        ▼
Rule 92004
        │
        ▼
Alert Generated
```

The rule correlates two conditions:

- Parent process must be **powershell.exe**.
- Child process must be **cmd.exe**.

When both conditions are satisfied, Rule **92004** generates the corresponding alert.

This validation confirms that native Wazuh detection already provides coverage for this behavior without requiring a custom detection rule.

---

# Detection Validation

The investigation confirmed that:

- Sysmon successfully recorded the Process Create event.
- Wazuh collected the telemetry.
- The Rules Engine processed the event correctly.
- Native Rule **92004** generated the expected alert.
- No custom detection rule was required.

---

# Technical Analysis

PowerShell spawning **cmd.exe** is a parent-child relationship commonly observed during administrative activities.

However, the same behavior is frequently abused by threat actors during post-exploitation to execute additional commands while leveraging trusted Windows binaries (LOLBins).

Because of this dual-use nature, the alert should always be analyzed in context before determining whether the activity is benign or malicious.

The investigation confirmed that the observed execution corresponded to a controlled laboratory simulation.

---

# MITRE ATT&CK

| Tactic | Technique |
|----------|-----------|
| Execution | T1059.003 – Windows Command Shell |

---

# Lessons Learned

- Parent-child process relationships provide valuable context during investigations.
- Native Wazuh rules already cover many common attack techniques.
- Detection validation should always precede custom rule development.
- Understanding rule dependencies simplifies Detection Engineering activities.
- Reviewing the official ruleset improves knowledge of the Wazuh detection engine.

---

# Conclusion

The validation confirmed that Wazuh provides native detection for command shell executions initiated by PowerShell through Rule **92004**.

The laboratory demonstrated the complete detection workflow, including Sysmon telemetry generation, event classification, rule evaluation and alert creation.

This project reinforces the importance of validating existing SIEM capabilities before implementing custom detection content and provides practical experience with Wazuh's native detection engine.

---

# Related Projects

- WI-002 – cmd.exe Execution
- TH-002 – LOLBins Activity
- CS-002 – Suspicious Command Prompt Investigation
