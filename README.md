# Cybersecurity Portfolio

<p align="center">
  <strong>SOC Operations · SIEM · Security Monitoring · Threat Hunting · Detection Engineering · Security Automation · AI-assisted Security Operations</strong>
</p>

<p align="center">
  Portafolio técnico basado en <strong>experiencia práctica de laboratorio</strong>, telemetría real generada en entornos controlados, automatización y documentación basada en evidencia.
</p>

<p align="center">
  <a href="https://github.com/fernando-jimenezh"><strong>Perfil profesional</strong></a> ·
  <a href="Projects/README.md"><strong>Investigaciones</strong></a> ·
  <a href="Projects/AI-Security-Automation/README.md"><strong>AI Security Automation</strong></a> ·
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

En paralelo, el laboratorio incorpora una línea de trabajo de **IA aplicada a operaciones técnicas**, donde el modelo interpreta solicitudes y una capa de control decide qué acciones pueden ejecutarse realmente.

```text
Solicitud en lenguaje natural
        ↓
LLM local
        ↓
Agente / API
        ↓
Validación y autorización
        ↓
Runner Linux controlado
        ↓
Tool autorizada
        ↓
Parser determinístico
        ↓
Resultado estructurado
        ↓
Interpretación por IA
```

> La documentación pública describe la arquitectura y las capacidades técnicas sin exponer identificadores internos, topología privada, credenciales, endpoints, información de clientes ni otros detalles operativos sensibles.

## Featured Projects

### AI-001 — Private AI Security Orchestration Lab

Diseño e implementación de una arquitectura privada de IA orientada a automatización y operaciones técnicas de seguridad.

**Demuestra:** Local LLM · Ollama · Web UI · REST API · Agent Architecture · Tool Orchestration · Linux · Security Controls · Deterministic Parsing

**Capacidades implementadas:**
- despliegue de un modelo LLM local;
- integración mediante interfaz Web;
- diseño de una capa de agente/API;
- separación entre razonamiento y ejecución;
- allowlist de tools y validación de parámetros;
- ejecución técnica en runner Linux aislado;
- auditoría y timeouts;
- parsing determinístico antes del análisis por IA;
- validación end-to-end de una operación técnica real.

**[Ver AI-001 →](Projects/AI-Security-Automation/AI-001-Private-AI-Security-Orchestration.md)**

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
| **Security Automation** | APIs, agents, tool execution, structured outputs y controles de ejecución |
| **Applied AI** | Local LLM deployment, orchestration, deterministic parsing y AI-assisted technical workflows |

## Investigaciones y proyectos

La sección `Projects` concentra la evidencia técnica principal:

```text
Projects/
├── AI-Security-Automation/     ← IA aplicada y automatización segura
├── Case-Studies/               ← investigaciones integrales
├── Windows-Investigations/     ← análisis de eventos y procesos
├── Detection-Rules/            ← validación de detecciones
└── Threat-Hunting-Reports/     ← hunting y correlación
```

**[Explorar todos los proyectos →](Projects/README.md)**

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
- Ollama.
- Open WebUI.
- REST APIs y agentes de automatización.

**[Ver construcción del laboratorio →](Labs/Foundation/Environment-Setup/README.md)**

## Tecnologías

`Wazuh` · `Sysmon` · `Suricata` · `Sigma` · `MITRE ATT&CK` · `Windows` · `Linux` · `Kali Linux` · `PowerShell` · `Bash` · `Ollama` · `Open WebUI` · `Local LLM` · `REST API` · `Git` · `GitHub`

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

Para proyectos de automatización e IA se añaden además:

- separación entre interpretación y ejecución;
- validación de parámetros;
- control de alcance;
- auditoría;
- resultados estructurados;
- protección de información sensible.

La evidencia y las conclusiones se mantienen separadas de las hipótesis. Si la información disponible no permite confirmar una afirmación, se documenta explícitamente como limitación.

## Estructura escalable

El portafolio continuará creciendo mediante nuevos casos y proyectos numerados:

```text
CS-001
CS-002
CS-003
...

AI-001
AI-002
AI-003
...
```

Los nuevos escenarios pueden incorporar investigaciones Windows/Linux, Detection Engineering, Threat Hunting, vulnerabilidades, network security, automatización e IA aplicada sin alterar la estructura principal del portafolio.

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
