# Security Investigations

Esta sección concentra las investigaciones prácticas desarrolladas en un laboratorio Blue Team controlado. Cada escenario se documenta desde diferentes perspectivas para demostrar cómo evoluciona un evento desde la telemetría inicial hasta una investigación completa.

<p align="center">
  <a href="../README.md"><strong>← Portafolio</strong></a> ·
  <a href="Case-Studies/README.md"><strong>Case Studies</strong></a> ·
  <a href="Windows-Investigations/README.md"><strong>Windows</strong></a> ·
  <a href="Detection-Rules/README.md"><strong>Detection</strong></a> ·
  <a href="Threat-Hunting-Reports/README.md"><strong>Threat Hunting</strong></a>
</p>

---

## Metodología

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

Los prefijos representan distintas capas de análisis del mismo entorno, no experiencia independiente inventada:

- **WI** — análisis técnico de eventos, procesos y telemetría Windows.
- **DR** — validación de lógica de detección y comportamiento del SIEM.
- **TH** — investigación proactiva para ampliar contexto y alcance.
- **CS** — caso integral que reúne evidencia, análisis, riesgo, timeline y conclusiones.

## Casos destacados

| Caso | Tema | Capacidades demostradas |
|---|---|---|
| **CS-001** | PowerShell EncodedCommand | Sysmon · Wazuh · Detection Validation · Threat Hunting · MITRE ATT&CK |
| **CS-002** | Suspicious Command Prompt | Windows Analysis · Process Investigation · SOC Assessment |
| **CS-003** | Windows Discovery | Discovery Commands · Detection · Threat Hunting · MITRE ATT&CK |

### Acceso directo

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

## Estructura para nuevos casos

El portafolio está preparado para continuar creciendo sin cambiar su navegación principal.

```text
Nuevo escenario
│
├── WI-00X   (si requiere investigación Windows)
├── DR-00X   (si requiere validación de detección)
├── TH-00X   (si requiere hunting)
└── CS-00X   (caso integral)
```

No todos los escenarios necesitan producir las cuatro piezas. Solo se publica la documentación que corresponda a evidencia realmente obtenida.

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

El criterio principal es **evidencia antes que suposiciones**.
