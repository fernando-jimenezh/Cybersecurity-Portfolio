# Cybersecurity Portfolio

<p align="center">
  <strong>SOC Operations · SIEM · Security Monitoring · Threat Hunting · Detection Engineering · Vulnerability Assessment · Network Security · Security Automation · AI-assisted Security Operations</strong>
</p>

<p align="center">
  Portafolio técnico basado en <strong>experiencia práctica de laboratorio</strong>, telemetría real generada en entornos controlados, evaluaciones autorizadas, automatización y documentación basada en evidencia.
</p>

<p align="center">
  <a href="https://github.com/fernando-jimenezh"><strong>Perfil profesional</strong></a> ·
  <a href="Projects/README.md"><strong>Investigaciones</strong></a> ·
  <a href="Labs/Foundation/Environment-Setup/README.md"><strong>Laboratorio</strong></a> ·
  <a href="Projects/AI-Security-Automation/README.md"><strong>AI Security Automation</strong></a> ·
  <a href="Knowledge-Base/README.md"><strong>Knowledge Base</strong></a>
</p>

---

## Qué demuestra este portafolio

Este repositorio documenta actividades realizadas en un laboratorio propio orientado a **ciberseguridad defensiva**. El objetivo es demostrar capacidades prácticas, reproducibles y trazables, no únicamente conocimiento teórico o uso aislado de herramientas.

El trabajo incluye construcción de infraestructura de monitoreo, generación y validación de telemetría, análisis SOC, Detection Validation, Threat Hunting, Network Security Monitoring, discovery controlado de activos y servicios, evaluación inicial de vulnerabilidades y automatización asistida por IA.

```text
Entorno controlado / scope autorizado
            ↓
Telemetría / Discovery
            ↓
Security Monitoring / Assessment
            ↓
Investigación y validación
            ↓
Detection / Threat Hunting
            ↓
Evidencia y conclusiones
```

---

## Metodología de aprendizaje e implementación

Las implementaciones y pruebas documentadas combinan:

- documentación técnica oficial de fabricantes y proyectos;
- manuales y referencias técnicas;
- práctica directa en entornos controlados;
- revisión de logs, servicios y resultados obtenidos;
- inteligencia artificial como apoyo para planificación, troubleshooting, contraste técnico y documentación.

La **IA se utiliza como herramienta de asistencia**, no como sustituto de la validación técnica. Los comandos, configuraciones, estados, evidencias y resultados relevantes se comprueban directamente en el laboratorio antes de documentarlos.

> La documentación pública describe capacidades y arquitectura sin exponer credenciales, endpoints internos, topologías privadas, información de clientes ni otros detalles operativos sensibles.

---

## Proyectos destacados

### AI-001 — Private AI Security Orchestration Lab

Diseño e implementación de una arquitectura privada de IA orientada a automatización y operaciones técnicas de seguridad.

**Demuestra:** Local LLM · Ollama · Web Interface · REST API · Agent Architecture · Tool Orchestration · Linux Runner · Security Controls · Deterministic Parsing

**[Ver AI-001 →](Projects/AI-Security-Automation/AI-001-Private-AI-Security-Orchestration.md)**

### CS-001 — PowerShell EncodedCommand Investigation

Investigación completa de un escenario `-EncodedCommand` compuesto por **tres pruebas controladas**:

1. validación de telemetría base;
2. Detection Validation de Wazuh Rule 92057;
3. Threat Hunting y repetibilidad.

La documentación diferencia correctamente los eventos observados de la alerta generada: se identificaron **3 eventos relacionados con `EncodedCommand` y 1 alerta Rule 92057**, porque la regla requiere condiciones adicionales, incluida la relación `powershell.exe → powershell.exe`.

**Demuestra:** Windows Event Analysis · Sysmon · Wazuh SIEM · Detection Validation · Threat Hunting · MITRE ATT&CK

**[Ver CS-001 →](Projects/Case-Studies/CS-001-Investigation-PowerShell-EncodedCommand.md)**

### CS-002 — Suspicious Command Prompt Investigation

Caso de análisis de ejecución de `cmd.exe` iniciada desde PowerShell, validando la relación parent-child process y la regla nativa Wazuh 92004.

**[Ver CS-002 →](Projects/Case-Studies/CS-002-Suspicious-Command-Prompt-Investigation.md)**

### CS-003 — Windows Discovery Investigation

Investigación centrada en `whoami.exe`, Discovery y validación de cobertura del ruleset, complementada con una regla personalizada cuando la cobertura nativa no era suficiente para ese escenario.

**[Ver CS-003 →](Projects/Case-Studies/CS-003-Windows-Discovery-Investigation.md)**

---

## Áreas de experiencia práctica

| Área | Evidencia disponible |
|---|---|
| **Security Monitoring** | Windows/Linux telemetry, log analysis, Wazuh SIEM |
| **Windows Investigation** | PowerShell, cmd, whoami, Sysmon Process Create |
| **Detection Engineering** | Validación de reglas Wazuh, lógica de detección, reglas personalizadas, MITRE ATT&CK |
| **Threat Hunting** | EncodedCommand, LOLBins, Windows Discovery |
| **Incident Investigation** | Timeline, evidence correlation, risk assessment, recommendations |
| **SIEM Administration** | Wazuh deployment, agents, telemetry, ruleset analysis |
| **Network Security Monitoring** | Suricata IDS, rules, `eve.json`, alert validation |
| **Asset & Service Discovery** | Nmap, host discovery, service discovery, scope control |
| **Vulnerability Assessment** | Attack surface review, controlled validation, evidence-based analysis |
| **Security Assessment Environment** | Kali Linux, isolated lab networks, controlled execution |
| **Security Automation** | APIs, agents, tool execution, structured outputs y controles de ejecución |
| **Applied AI** | Local LLM deployment, orchestration, deterministic parsing y AI-assisted technical workflows |

---

## Laboratorios destacados

### Security Foundations

- [Wazuh SIEM Deployment](Labs/Foundation/Wazuh-Deployment/README.md)
- [Windows & Linux Telemetry Collection](Labs/Foundation/Telemetry-Collection/README.md)
- [Cybersecurity Lab Environment](Labs/Foundation/Environment-Setup/README.md)

### Network Security

- [Suricata IDS — Network Security Monitoring](Labs/Network-Security/Suricata-IDS/README.md)

### Security Assessment

- [Kali Linux — Controlled Security Assessment Environment](Labs/Security-Assessment/Kali-Controlled-Assessment/README.md)
- [Asset & Service Discovery — Controlled Security Assessment](Labs/Security-Assessment/Asset-Service-Discovery/README.md)
- [Vulnerability Assessment — Controlled Security Validation](Labs/Security-Assessment/Vulnerability-Assessment/README.md)

---

## Investigaciones y proyectos

La sección `Projects` concentra investigaciones donde las capacidades construidas en los laboratorios se aplican a actividades concretas de ciberseguridad.

```text
Projects/
├── AI-Security-Automation/     ← IA aplicada y automatización segura
├── Case-Studies/               ← investigaciones integrales
├── Windows-Investigations/     ← análisis de eventos y procesos
├── Linux-Investigations/       ← investigaciones Linux
├── Detection-Rules/            ← validación y desarrollo de detecciones
└── Threat-Hunting-Reports/     ← hunting y correlación
```

**[Explorar todos los proyectos →](Projects/README.md)**

---

## Arquitectura general del laboratorio

```text
Kali Linux / actividad controlada
          │
          ├──────────────► Asset & Service Discovery
          │                         │
          │                         ▼
          │                 Vulnerability Assessment
          │
          ▼
Windows 11 / Ubuntu
          │
          ├── Windows Event Logs / Sysmon
          └── auditd / Syslog / systemd journal
          │
          ▼
      Wazuh Agents
          │
          ▼
      Wazuh Manager
          │
          ▼
      Wazuh Indexer
          │
          ▼
      Wazuh Dashboard
          │
          ▼
SOC Analysis / Detection / Threat Hunting / IR

Network traffic
      │
      ▼
Suricata IDS
      │
      ▼
eve.json / alerts
      │
      └──► Network Security Monitoring
           └──► integración SIEM como evolución del laboratorio
```

> La relación Suricata → SIEM se mantiene documentada como **integración prevista/conceptual** mientras no exista evidencia publicada de ingestión real de `eve.json` en Wazuh.

---

## Componentes utilizados

- Wazuh SIEM.
- Windows 11.
- Ubuntu Server.
- Kali Linux.
- Sysmon.
- Windows Event Logs.
- auditd.
- Syslog.
- systemd journal / `journalctl`.
- Suricata.
- Nmap.
- VirtualBox.
- PowerShell / Bash.
- Ollama.
- Open WebUI.
- REST APIs y agentes de automatización.

---

## Tecnologías

`Wazuh` · `Sysmon` · `Suricata` · `Nmap` · `Kali Linux` · `Sigma` · `MITRE ATT&CK` · `Windows` · `Linux` · `PowerShell` · `Bash` · `Ollama` · `Open WebUI` · `Local LLM` · `REST API` · `Git` · `GitHub`

---

## Principios de documentación

Todo trabajo publicado debe cumplir, cuando corresponda, con:

- objetivo y alcance;
- entorno controlado o scope autorizado;
- evidencia observada;
- análisis técnico;
- separación entre evento, alerta, evidencia e hipótesis;
- validación de resultados;
- conclusiones y recomendaciones;
- protección de información sensible;
- referencias y relación con otros laboratorios o casos.

Para evaluaciones de seguridad se añaden:

- validación previa de targets;
- control de IP/CIDR y alcance;
- preferencia por pruebas no destructivas y read-only;
- trazabilidad de ejecución;
- revisión manual de resultados relevantes.

Para automatización e IA se añaden:

- separación entre interpretación y ejecución;
- validación de parámetros;
- allowlisting y control de alcance;
- auditoría y timeouts;
- resultados estructurados;
- validación técnica independiente de la salida del modelo.

---

## Estructura escalable

Los nuevos escenarios se incorporan únicamente cuando existe trabajo práctico y evidencia que los respalde. El portafolio prioriza calidad, trazabilidad y consistencia técnica sobre cantidad de documentos.

---

## Knowledge Base

La Knowledge Base conserva notas y fundamentos técnicos relacionados directamente con tecnologías y metodologías utilizadas en el laboratorio.

**[Explorar Knowledge Base →](Knowledge-Base/README.md)**

---

## Perfil profesional

Este repositorio contiene evidencia técnica y experiencia práctica de laboratorio orientada a ciberseguridad.

Para experiencia profesional, formación, competencias, CV y credenciales:

<p align="center">
  <strong><a href="https://github.com/fernando-jimenezh">github.com/fernando-jimenezh</a></strong>
</p>

---

© 2026 Lenin Fernando Jiménez Herrera
