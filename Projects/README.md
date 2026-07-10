# Projects

## Overview

This section contains practical cybersecurity investigations developed in a personal Blue Team laboratory using **Wazuh SIEM**, **Sysmon**, and **Windows 11**.

The objective of these projects is to demonstrate technical capabilities in:

- Security Monitoring
- Windows Event Analysis
- Detection Engineering
- Threat Hunting
- Incident Investigation
- Blue Team Operations

All investigations are based on telemetry collected from the laboratory and documented using a standardized methodology.

---

# Investigation Methodology

Each security scenario follows the same investigation workflow.

```text
Windows Activity
        │
        ▼
Telemetry Collection
(Sysmon)
        │
        ▼
Security Monitoring
(Wazuh SIEM)
        │
        ▼
Windows Investigation (WI)
        │
        ▼
Detection Rule Validation (DR)
        │
        ▼
Threat Hunting (TH)
        │
        ▼
Case Study (CS)
```

This methodology simulates the workflow commonly performed by Security Operations Center (SOC) analysts when investigating security events.

---

# Project Categories

## Windows Investigations (WI)

Windows Investigations focus on the analysis of individual events collected through Sysmon and Wazuh.

Each investigation includes:

- Event identification
- Telemetry analysis
- Process investigation
- Parent-child process relationships
- MITRE ATT&CK mapping
- SOC analyst assessment

Current investigations

| ID | Investigation |
|----|---------------|
| WI-001 | PowerShell EncodedCommand |
| WI-002 | Command Prompt Execution |
| WI-003 | whoami Enumeration |

---

## Detection Rules (DR)

Detection Rule projects validate how Wazuh detects a specific technique.

These projects include:

- Native rule validation
- Ruleset analysis
- Detection logic
- Custom rule development (when required)
- Detection testing

Current projects

| ID | Project |
|----|----------|
| DR-001 | Validate Native Rule 92057 |
| DR-002 | Validate Native Rule 92004 |
| DR-003 | Detect whoami Enumeration |

---

## Threat Hunting Reports (TH)

Threat Hunting projects expand the investigation beyond the initial alert.

Typical hunting activities include:

- Searching for similar executions
- Identifying affected endpoints
- Reviewing related users
- Correlating parent-child processes
- Evaluating the scope of the activity

Current reports

| ID | Investigation |
|----|---------------|
| TH-001 | PowerShell EncodedCommand |
| TH-002 | LOLBins Activity |
| TH-003 | Windows Discovery Commands |

---

## Case Studies (CS)

Case Studies consolidate all previous investigations into a complete security investigation.

Each case study combines:

- Windows Investigation
- Detection Validation
- Threat Hunting
- Technical Analysis
- Risk Assessment
- Conclusions
- Lessons Learned

Current case studies

| ID | Investigation |
|----|---------------|
| CS-001 | PowerShell EncodedCommand Investigation |
| CS-002 | Suspicious Command Prompt Investigation |
| CS-003 | Windows Discovery Investigation |

---

# Standard Investigation Structure

Every project follows the same documentation format.

- Executive Summary
- Objective
- Environment
- Scenario
- Evidence
- Technical Analysis
- Detection Validation (when applicable)
- Threat Hunting Assessment (when applicable)
- MITRE ATT&CK Mapping
- Risk Assessment
- Recommendations
- Lessons Learned
- Conclusion
- References
- Related Projects

---

# Technologies Used

- Wazuh SIEM
- Sysmon
- Windows 11
- VirtualBox
- PowerShell
- Windows Event Logs
- MITRE ATT&CK

---

# Repository Goal

The purpose of this repository is to document practical cybersecurity investigations that demonstrate skills related to:

- Security Monitoring
- SOC Operations
- Detection Engineering
- Threat Hunting
- Incident Investigation
- Windows Security
- Blue Team Methodologies

Each investigation is based on real telemetry generated within the laboratory and follows a repeatable investigation methodology similar to that used by Security Operations Centers (SOC).
