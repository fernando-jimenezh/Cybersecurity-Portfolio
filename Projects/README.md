# Security Projects & Investigations

Esta sección concentra investigaciones prácticas y proyectos técnicos desarrollados en un laboratorio Blue Team controlado. Cada escenario se documenta para demostrar capacidades reales, trazables y basadas en evidencia.

<p align="center">
  <a href="../README.md"><strong>← Portafolio</strong></a> ·
  <a href="AI-Security-Automation/README.md"><strong>AI Security Automation</strong></a> ·
  <a href="Case-Studies/README.md"><strong>Case Studies</strong></a> ·
  <a href="Windows-Investigations/README.md"><strong>Windows</strong></a> ·
  <a href="Detection-Rules/README.md"><strong>Detection</strong></a> ·
  <a href="Threat-Hunting-Reports/README.md"><strong>Threat Hunting</strong></a>
</p>

---

## Líneas de trabajo

### AI Security Automation

Proyectos orientados a integrar IA local con operaciones técnicas de forma controlada, utilizando agentes, APIs, validación de parámetros, ejecución autorizada, auditoría y parsers determinísticos.

| ID | Proyecto | Capacidades demostradas |
|---|---|---|
| **AI-001** | [Private AI Security Orchestration Lab](AI-Security-Automation/AI-001-Private-AI-Security-Orchestration.md) | Local LLM · Ollama · Web UI · API · Agents · Tool Orchestration · Linux · Security Controls |

> Los documentos públicos de esta categoría omiten deliberadamente nombres internos, direcciones de red, endpoints privados, credenciales, rutas sensibles, detalles de clientes y otros elementos operativos que no son necesarios para demostrar la capacidad técnica.

---

## Metodología de investigación defensiva

```text
Actividad observada
        │
        ▼
Windows Investigation (WI)
        │
        ▼
Detection Validation (DR)
        │
        ▼
Threat Hunting (TH)
        │
        ▼
Case Study (CS)
```

Los prefijos representan distintas capas de análisis del mismo entorno:

- **WI** — análisis técnico de eventos, procesos y telemetría Windows.
- **DR** — validación de lógica de detección y comportamiento del SIEM.
- **TH** — investigación proactiva para ampliar contexto y alcance.
- **CS** — caso integral que reúne evidencia, análisis, riesgo, timeline y conclusiones.
- **AI** — proyectos de IA aplicada, automatización segura y orquestación técnica.

## Casos destacados

| Caso | Tema | Capacidades demostradas |
|---|---|---|
| **AI-001** | Private AI Security Orchestration | Local LLM · API · Agent · Security Automation · Deterministic Parsing |
| **CS-001** | PowerShell EncodedCommand | Sysmon · Wazuh · Detection Validation · Threat Hunting · MITRE ATT&CK |
| **CS-002** | Suspicious Command Prompt | Windows Analysis · Process Investigation · SOC Assessment |
| **CS-003** | Windows Discovery | Discovery Commands · Detection · Threat Hunting · MITRE ATT&CK |

### Acceso directo

- **[AI-001 — Private AI Security Orchestration](AI-Security-Automation/AI-001-Private-AI-Security-Orchestration.md)**
- **[CS-001 — PowerShell EncodedCommand](Case-Studies/CS-001-Investigation-PowerShell-EncodedCommand.md)**
- **[CS-002 — Suspicious Command Prompt](Case-Studies/CS-002-Suspicious-Command-Prompt-Investigation.md)**
- **[CS-003 — Windows Discovery](Case-Studies/CS-003-Windows-Discovery-Investigation.md)**

## Windows Investigations

| ID | Investigación |
|---|---|
| **WI-001** | [PowerShell EncodedCommand](Windows-Investigations/WI-001-PowerShell-EncodedCommand.md) |
| **WI-002** | [Command Prompt Execution](Windows-Investigations/WI-002-cmd-Execution.md) |
| **WI-003** | [whoami Enumeration](Windows-Investigations/WI-003-whoami-Enumeration.md) |

## Detection Validation

| ID | Validación |
|---|---|
| **DR-001** | [Wazuh Rule 92057 — PowerShell EncodedCommand](Detection-Rules/DR-001-Validate-Wazuh-Rule-92057-PowerShell-EncodedCommand.md) |
| **DR-002** | [Wazuh Rule 92004 — PowerShell spawning Command Prompt](Detection-Rules/DR-002-Validate-Wazuh-Rule-92004-PowerShell-Spawning-Command-Prompt.md) |
| **DR-003** | [whoami Enumeration](Detection-Rules/DR-003-Detect-whoami-Enumeration.md) |

## Threat Hunting Reports

| ID | Investigación |
|---|---|
| **TH-001** | [PowerShell EncodedCommand](Threat-Hunting-Reports/TH-001-PowerShell-EncodedCommand.md) |
| **TH-002** | [LOLBins Activity](Threat-Hunting-Reports/TH-002-LOLBins-Activity.md) |
| **TH-003** | [Windows Discovery Commands](Threat-Hunting-Reports/TH-003-Windows-Discovery-Commands.md) |

## Estructura para nuevos proyectos

El portafolio está preparado para continuar creciendo sin cambiar su navegación principal.

```text
Nuevo escenario defensivo
│
├── WI-00X   (si requiere investigación Windows)
├── DR-00X   (si requiere validación de detección)
├── TH-00X   (si requiere hunting)
└── CS-00X   (caso integral)

Nuevo proyecto de IA / automatización
│
└── AI-00X
```

No todos los escenarios necesitan producir todas las piezas. Solo se publica documentación respaldada por trabajo y evidencia realmente obtenidos.

## Estándar documental

Los casos deben incluir, cuando aplique:

- resumen ejecutivo;
- objetivo y alcance;
- entorno;
- escenario;
- evidencia;
- análisis técnico;
- Detection Validation;
- Threat Hunting;
- MITRE ATT&CK mapping;
- evaluación de riesgo;
- recomendaciones;
- lecciones aprendidas;
- conclusión;
- referencias;
- proyectos relacionados.

Los proyectos de IA y automatización deben documentar además:

- arquitectura lógica;
- separación entre razonamiento y ejecución;
- controles de autorización;
- validación de entradas;
- auditoría y timeouts;
- parsing y resultados estructurados;
- limitaciones;
- criterios de protección de información sensible.

El criterio principal es **evidencia antes que suposiciones**.
