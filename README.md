# Cybersecurity Portfolio

<p align="center">
  <strong>SOC Operations · SIEM · Security Monitoring · Threat Hunting · Detection Engineering · Incident Investigation</strong>
</p>

<p align="center">
  Portafolio técnico basado en <strong>experiencia práctica de laboratorio</strong>, telemetría real generada en entornos controlados y documentación basada en evidencia.
</p>

<p align="center">
  <a href="https://github.com/fernando-jimenezh"><strong>Perfil profesional</strong></a> ·
  <a href="Projects/README.md"><strong>Investigaciones</strong></a> ·
  <a href="Labs/Foundation/Environment-Setup/README.md"><strong>Laboratorio</strong></a> ·
  <a href="Knowledge-Base/README.md"><strong>Knowledge Base</strong></a>
</p>

---

## Qué demuestra este portafolio

Este repositorio documenta actividades realizadas en un laboratorio propio orientado a ciberseguridad defensiva. El objetivo es demostrar capacidades prácticas y trazables, no únicamente conocimiento teórico o uso aislado de herramientas.

Las investigaciones siguen un flujo basado en evidencia:

```text
Actividad controlada
        ↓
Telemetría
        ↓
Security Monitoring
        ↓
Investigación
        ↓
Detection Validation
        ↓
Threat Hunting
        ↓
MITRE ATT&CK
        ↓
Conclusiones y recomendaciones
```

## Featured Case Studies

### CS-001 — PowerShell EncodedCommand Investigation

Investigación completa de una ejecución PowerShell con `-EncodedCommand`.

**Demuestra:** Windows Event Analysis · Sysmon · Wazuh SIEM · Detection Validation · Threat Hunting · MITRE ATT&CK

**Evidencia destacada:**
- Sysmon Event ID 1.
- Proceso `powershell.exe` y proceso padre `cmd.exe`.
- Validación de Wazuh Rule 92057.
- Análisis del flujo `18100 → 184665 → sysmon_event1 → 92057`.
- Hunting sobre actividad PowerShell y EncodedCommand.
- MITRE ATT&CK T1059.001.

**[Ver CS-001 →](Projects/Case-Studies/CS-001-Investigation-PowerShell-EncodedCommand.md)**

### CS-002 — Suspicious Command Prompt Investigation

Caso de análisis de ejecución de `cmd.exe`, telemetría relacionada y evaluación desde la perspectiva de un analista SOC.

**[Ver CS-002 →](Projects/Case-Studies/CS-002-Suspicious-Command-Prompt-Investigation.md)**

### CS-003 — Windows Discovery Investigation

Investigación centrada en comandos de discovery y enumeración en Windows, correlacionando comportamiento, telemetría y contexto defensivo.

**[Ver CS-003 →](Projects/Case-Studies/CS-003-Windows-Discovery-Investigation.md)**

---

## Áreas de experiencia práctica

| Área | Evidencia disponible |
|---|---|
| **Security Monitoring** | Windows/Linux telemetry, log analysis, Wazuh SIEM |
| **Windows Investigation** | PowerShell, cmd, whoami, Sysmon Process Create |
| **Detection Engineering** | Validación de reglas Wazuh, lógica de detección, MITRE ATT&CK |
| **Threat Hunting** | EncodedCommand, LOLBins, Windows Discovery |
| **Incident Investigation** | Timeline, evidence correlation, risk assessment, recommendations |
| **SIEM Administration** | Wazuh deployment, agents, telemetry, ruleset analysis |

## Investigaciones

La sección `Projects` contiene la evidencia técnica principal y está organizada en cuatro perspectivas complementarias:

```text
Projects/
├── Case-Studies/              ← investigaciones integrales
├── Windows-Investigations/    ← análisis de eventos y procesos
├── Detection-Rules/           ← validación de detecciones
└── Threat-Hunting-Reports/    ← hunting y correlación
```

**[Explorar todas las investigaciones →](Projects/README.md)**

## Laboratorio

El laboratorio permite generar y analizar telemetría de forma controlada.

```text
Kali Linux
    │
    ▼
Windows 11 / Ubuntu
    │
    ▼
Sysmon / auditd / logs
    │
    ▼
Wazuh SIEM
    │
    ▼
SOC Analysis
```

Componentes utilizados:

- Wazuh SIEM.
- Windows 11.
- Ubuntu Server.
- Kali Linux.
- Sysmon.
- Suricata.
- VirtualBox.
- PowerShell / Bash.

**[Ver construcción del laboratorio →](Labs/Foundation/Environment-Setup/README.md)**

## Tecnologías

`Wazuh` · `Sysmon` · `Suricata` · `Sigma` · `MITRE ATT&CK` · `Windows` · `Linux` · `Kali Linux` · `PowerShell` · `Bash` · `Git` · `GitHub`

## Principios de documentación

Todo caso publicado debe cumplir, cuando corresponda, con:

- objetivo y alcance;
- entorno controlado;
- evidencia observada;
- análisis técnico;
- Detection Validation;
- Threat Hunting;
- MITRE ATT&CK mapping;
- evaluación del analista;
- conclusiones y recomendaciones;
- referencias y relación con otros casos.

La evidencia y las conclusiones se mantienen separadas de las hipótesis. Si la información disponible no permite confirmar una afirmación, se documenta explícitamente como limitación.

## Estructura escalable

El portafolio continuará creciendo mediante nuevos casos numerados:

```text
CS-001
CS-002
CS-003
CS-004
...
```

Los nuevos escenarios pueden incorporar investigaciones Windows/Linux, Detection Engineering, Threat Hunting, vulnerabilidades, network security y otras áreas defensivas sin alterar la estructura principal del portafolio.

## Knowledge Base

La Knowledge Base conserva notas y fundamentos técnicos relacionados directamente con las tecnologías y metodologías utilizadas en el laboratorio.

**[Explorar Knowledge Base →](Knowledge-Base/README.md)**

---

## Perfil profesional

Este repositorio contiene exclusivamente evidencia técnica y experiencia práctica de laboratorio.

Para experiencia profesional, formación, competencias, CV y credenciales:

<p align="center">
  <strong><a href="https://github.com/fernando-jimenezh">github.com/fernando-jimenezh</a></strong>
</p>

---

© 2026 Lenin Fernando Jiménez Herrera
