# CS-001 — Investigación de PowerShell EncodedCommand

## Resumen ejecutivo

Este caso documenta un escenario de **PowerShell `-EncodedCommand`** compuesto por **tres pruebas controladas** realizadas dentro del laboratorio.

El objetivo fue validar, de forma progresiva, la telemetría generada por Sysmon, el procesamiento de eventos en Wazuh, la activación de la regla nativa **92057** y la capacidad de ampliar el análisis mediante **Threat Hunting**.

Las tres pruebas produjeron evidencia relacionada, pero no idéntica. En particular, una ejecución tuvo `cmd.exe` como proceso padre, mientras que la ejecución que activó la regla 92057 requirió la relación `powershell.exe → powershell.exe -EncodedCommand ...`. Esta separación corrige una asociación anterior en la documentación donde evidencias de pruebas distintas aparecían como si correspondieran al mismo evento.

---

## Objetivo

- Validar la generación de telemetría de PowerShell mediante Sysmon.
- Confirmar la recepción y procesamiento en Wazuh.
- Comprender la lógica de la regla nativa 92057.
- Diferenciar eventos observados de alertas generadas.
- Correlacionar las tres pruebas dentro de una investigación única y coherente.

---

## Entorno

| Componente | Valor |
|---|---|
| Sistema operativo | Windows 11 |
| SIEM | Wazuh 4.14.5 |
| Telemetría | Sysmon |
| Hipervisor | VirtualBox |

---

## Escenario y pruebas realizadas

### Prueba 1 — Telemetría base

Se ejecutó PowerShell desde `cmd.exe` utilizando:

```powershell
powershell.exe -EncodedCommand QQA=
```

La ejecución generó **Sysmon Event ID 1** y permitió comprobar que la línea de comandos, proceso padre, usuario e Integrity Level quedaban disponibles para análisis.

Relación observada:

```text
cmd.exe
  ↓
powershell.exe -EncodedCommand QQA=
```

Esta prueba validó telemetría, pero no representa el evento exacto que activó Wazuh Rule 92057, porque la regla requiere `powershell.exe` como proceso padre.

### Prueba 2 — Detection Validation

Se reprodujo el escenario desde una sesión PowerShell para generar la relación requerida por la regla:

```text
powershell.exe
      ↓
powershell.exe -EncodedCommand QQA=
```

Esta ejecución cumplió la lógica de la regla nativa **92057** y generó la alerta correspondiente.

### Prueba 3 — Threat Hunting y repetibilidad

Se realizaron búsquedas sobre el período de pruebas para determinar cuántos eventos relacionados existían.

Resultados consolidados:

- **3 eventos** con `EncodedCommand`.
- **10 ejecuciones** de PowerShell observadas en el período analizado.
- **1 alerta** correspondiente a `rule.id:92057`.
- Actividad limitada al endpoint del laboratorio.

La diferencia entre tres eventos y una alerta es coherente: la regla evalúa condiciones adicionales, incluida la relación entre proceso padre e hijo.

---

## Sobre la cadena Base64 utilizada

La cadena:

```text
QQA=
```

es **Base64 válida**. Interpretada con la codificación UTF-16LE esperada por Windows PowerShell para `-EncodedCommand`, representa el texto `A`.

El propósito del laboratorio no fue ejecutar una carga maliciosa, sino generar una acción mínima y controlada que permitiera producir telemetría y validar detecciones. Por ello, el contenido utilizado no debe describirse como “Base64 inválido”.

---

## Evidencia de la Prueba 1

| Campo | Valor |
|---|---|
| Provider | Microsoft-Windows-Sysmon |
| Event ID | 1 |
| Image | `powershell.exe` |
| Parent Image | `cmd.exe` |
| Command Line | `powershell.exe -EncodedCommand QQA=` |
| User | `DESKTOP-7CLFI8R\lab` |
| Integrity Level | High |

Esta evidencia demuestra la captura de telemetría, pero no debe utilizarse como representación del evento de la Prueba 2 que generó Rule 92057.

---

## Evidencia de Detection Validation

La regla nativa Wazuh 92057 en la versión 4.14.5 exige, de forma resumida:

```text
Sysmon Event ID 1
      ↓
Group sysmon_event1
      ↓
Parent Image = powershell.exe
      ↓
CommandLine = powershell.exe ... -EncodedCommand ...
      ↓
Rule 92057
      ↓
Security Alert
```

La regla tiene **level 12** y está mapeada a **MITRE ATT&CK T1059.001 — PowerShell**.

---

## Análisis técnico

`-EncodedCommand` permite entregar a PowerShell contenido codificado en Base64. La codificación Base64 no cifra la información, pero puede utilizarse como mecanismo de **command obfuscation**.

Este comportamiento tiene naturaleza **dual-use**:

- puede aparecer en automatización y administración legítima;
- también puede utilizarse para dificultar la lectura inmediata de comandos durante actividad ofensiva.

Por ello, una detección correcta requiere contexto adicional, como:

- proceso padre e hijos;
- usuario;
- Integrity Level;
- frecuencia de ejecución;
- actividad de red;
- eventos posteriores;
- detecciones relacionadas.

---

## Threat Hunting Assessment

La revisión ampliada confirmó que:

- las tres ejecuciones se mantuvieron dentro del laboratorio;
- solo una cumplió las condiciones de Rule 92057;
- no se identificaron otros endpoints afectados;
- no se observó evidencia de movimiento lateral;
- no se identificaron mecanismos de persistencia asociados;
- no se identificó evidencia adicional de compromiso dentro del alcance y período analizados.

---

## Evaluación de riesgo

| Factor | Evaluación |
|---|---|
| Probabilidad | Baja dentro del escenario controlado |
| Impacto | Bajo dentro del escenario controlado |
| Prioridad | Informativa / validación técnica |

En un entorno empresarial real, una alerta de este tipo debe evaluarse según contexto, usuario, proceso padre, payload, actividad de red y comportamiento posterior.

---

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| Execution | **T1059.001 — PowerShell** |
| Defense Evasion / contexto de ofuscación | **T1027.010 — Command Obfuscation** |

> T1059.001 corresponde al mapeo directo utilizado por la regla Wazuh 92057. T1027.010 se utiliza como contexto adicional para describir el posible empleo de contenido codificado u ofuscado.

---

## Recomendaciones

- Correlacionar `EncodedCommand` con procesos padre e hijos.
- Revisar PowerShell Script Block Logging cuando esté disponible.
- Analizar conexiones de red y procesos posteriores.
- Diferenciar siempre entre evento observado y alerta generada.
- Validar el contenido nativo del SIEM antes de crear reglas personalizadas.
- Conservar evidencia por prueba para evitar asociaciones incorrectas durante investigaciones posteriores.

---

## Lecciones aprendidas

- Una misma técnica puede generar eventos diferentes según la cadena de procesos.
- No todos los eventos que contienen `-EncodedCommand` cumplen la lógica de una regla específica.
- La evidencia debe correlacionarse por timestamp, proceso padre, Process ID y demás campos relevantes antes de atribuir una alerta.
- Base64 es codificación, no cifrado.
- Detection Validation y Threat Hunting se complementan: la primera comprueba la regla y el segundo amplía el contexto.

---

## Conclusión

El escenario confirmó correctamente el funcionamiento conjunto de **Sysmon**, **Wazuh**, **Detection Engineering** y **Threat Hunting** mediante tres pruebas relacionadas.

La primera prueba validó la telemetría de PowerShell iniciada desde `cmd.exe`; la segunda reprodujo la relación requerida por la regla nativa 92057 y confirmó la detección; la tercera permitió contextualizar los resultados y explicar por qué se observaron tres eventos con `EncodedCommand`, pero solo una alerta 92057.

La documentación queda así alineada con la evidencia disponible y con la lógica técnica del ruleset de Wazuh 4.14.5.

---

## Proyectos relacionados

- **WI-001** — PowerShell EncodedCommand.
- **DR-001** — Validate Wazuh Rule 92057.
- **TH-001** — Threat Hunting: PowerShell EncodedCommand.
