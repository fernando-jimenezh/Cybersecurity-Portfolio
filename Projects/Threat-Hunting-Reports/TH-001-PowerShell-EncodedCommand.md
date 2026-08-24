# TH-001 — Threat Hunting: PowerShell EncodedCommand

## Resumen ejecutivo

Durante las actividades de **Threat Hunting** se investigaron ejecuciones de **PowerShell** que utilizaron el parámetro `-EncodedCommand` dentro de un laboratorio controlado.

El objetivo fue determinar si la actividad observada correspondía únicamente a pruebas aisladas o si existían eventos relacionados que justificaran ampliar la investigación.

La búsqueda identificó **3 eventos asociados a `EncodedCommand`**, mientras que solo **1 de ellos activó la regla nativa Wazuh 92057**. Esta diferencia es coherente con la lógica de la regla: no basta con que aparezca `-EncodedCommand`; también debe cumplirse la relación de proceso padre e hijo requerida por la detección.

---

## Relación con las tres pruebas realizadas

| Prueba | Objetivo | Resultado |
|---|---|---|
| **Prueba 1 — Telemetría base** | Validar Sysmon/Wazuh con PowerShell iniciado desde `cmd.exe` | Evento registrado; no cumple `parentImage = powershell.exe` |
| **Prueba 2 — Detection Validation** | Generar una relación `powershell.exe → powershell.exe -EncodedCommand ...` | **Rule 92057** activada |
| **Prueba 3 — Threat Hunting / repetibilidad** | Buscar todas las ejecuciones relacionadas | 3 eventos `EncodedCommand`; 1 alerta 92057 |

---

## Objetivo

Determinar si las ejecuciones de PowerShell con `-EncodedCommand`:

- estaban limitadas al endpoint de laboratorio;
- correspondían a pruebas controladas;
- generaban actividad adicional relevante;
- producían detecciones nativas consistentes con la lógica del ruleset;
- presentaban señales de persistencia, movimiento lateral u otra actividad no esperada.

---

## Hipótesis de investigación

El uso de `-EncodedCommand` puede observarse tanto en automatización legítima como en actividades ofensivas. La codificación Base64 no es cifrado, pero puede utilizarse para **command obfuscation**.

**Hipótesis:**

> Si una ejecución codificada correspondiera a una actividad maliciosa más amplia, deberían existir otros eventos relacionados en procesos, usuarios, endpoints, conexiones o mecanismos de persistencia.

---

## Entorno

| Componente | Valor |
|---|---|
| Sistema operativo | Windows 11 |
| SIEM | Wazuh 4.14.5 |
| Telemetría | Sysmon |
| Hipervisor | VirtualBox |

---

## Metodología

La investigación amplió el análisis desde la evidencia inicial para revisar:

- número de ejecuciones con `EncodedCommand`;
- actividad total de PowerShell;
- reglas de detección activadas;
- endpoints afectados;
- usuarios involucrados;
- procesos padre e hijos;
- actividad posterior relacionada.

---

## Hunting Queries

### Ejecuciones con EncodedCommand

```kql
data.win.eventdata.commandLine:*EncodedCommand*
```

**Resultado:**

- **3 eventos identificados.**

### Actividad total de PowerShell

```kql
data.win.eventdata.image:*powershell.exe*
```

**Resultado:**

- **10 ejecuciones de PowerShell observadas.**

### Regla de detección

```kql
rule.id:92057
```

**Resultado:**

- **1 alerta generada.**

### Endpoint

```kql
agent.name:W11-Lab
```

**Resultado:**

- Actividad limitada al endpoint del laboratorio.

### Usuario

```kql
data.win.eventdata.user:*
```

Usuario principal observado:

```text
DESKTOP-7CLFI8R\lab
```

---

## Hallazgos

La investigación determinó que:

- se observaron tres eventos con `EncodedCommand`;
- las tres ejecuciones no eran idénticas desde el punto de vista de la relación **parent-child process**;
- una de las pruebas registró `cmd.exe` como proceso padre;
- la ejecución que cumplió la lógica `powershell.exe → powershell.exe -EncodedCommand ...` activó la regla **92057**;
- no se identificaron otros endpoints afectados;
- no se observó evidencia de movimiento lateral;
- no se identificaron mecanismos de persistencia asociados;
- la actividad permaneció dentro del entorno controlado.

---

## Indicadores revisados

### Proceso

```text
powershell.exe
```

### Línea de comandos de referencia

```text
powershell.exe -EncodedCommand QQA=
```

### Relaciones de proceso observadas durante las pruebas

```text
Prueba de telemetría base:
cmd.exe
  ↓
powershell.exe -EncodedCommand ...

Prueba de Detection Validation:
powershell.exe
  ↓
powershell.exe -EncodedCommand ...
```

La segunda relación es la que satisface la condición de la regla Wazuh 92057.

---

## Evaluación de Threat Hunting

No se identificó evidencia que indicara un compromiso activo dentro del alcance y período revisados.

Las ejecuciones correspondieron a pruebas controladas orientadas a validar telemetría, Detection Engineering y capacidad de investigación. La existencia de tres eventos y una sola alerta no constituye una contradicción: refleja que la regla 92057 evalúa condiciones adicionales además de la presencia de `-EncodedCommand`.

---

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| Execution | **T1059.001 — PowerShell** |
| Defense Evasion | **T1027.010 — Command Obfuscation** |

---

## Recomendaciones

- Continuar correlacionando `EncodedCommand` con procesos padre e hijos.
- Revisar **PowerShell Script Block Logging** cuando esté disponible.
- Correlacionar con conexiones de red y actividad posterior.
- Diferenciar siempre entre evento observado y alerta generada.
- Mantener búsquedas de hunting que permitan detectar variaciones de la misma técnica.

---

## Lecciones aprendidas

- Una búsqueda amplia puede encontrar más eventos que una regla específica.
- La relación **parent-child process** puede ser determinante para una detección.
- Base64 representa codificación, no cifrado.
- Threat Hunting aporta contexto que una alerta aislada no proporciona.
- La evidencia debe mantenerse separada por prueba antes de correlacionarse.

---

## Conclusión

La actividad de Threat Hunting confirmó que el escenario estuvo compuesto por **tres pruebas controladas relacionadas**, no por una única ejecución repetida de forma idéntica.

Se identificaron tres eventos con `EncodedCommand`, de los cuales uno cumplió las condiciones necesarias para generar **Wazuh Rule 92057**. No se identificaron indicadores adicionales de compromiso dentro del alcance analizado.

El ejercicio demuestra la utilidad conjunta de **Sysmon**, **Wazuh**, **Detection Validation** y **Threat Hunting** para comprender por qué determinados eventos generan alertas y otros no.

---

## Proyectos relacionados

- **WI-001** — PowerShell EncodedCommand.
- **DR-001** — Validate Wazuh Rule 92057.
- **CS-001** — PowerShell EncodedCommand Investigation.
