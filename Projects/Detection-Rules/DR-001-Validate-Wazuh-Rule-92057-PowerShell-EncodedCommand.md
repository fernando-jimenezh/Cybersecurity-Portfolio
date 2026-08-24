# DR-001 — Validate Wazuh Rule 92057 — PowerShell EncodedCommand

## Resumen ejecutivo

Este proyecto valida la regla nativa **Wazuh Rule 92057**, orientada a detectar ejecuciones de **PowerShell** en las que un proceso `powershell.exe` inicia otro proceso PowerShell utilizando `-EncodedCommand` o abreviaciones compatibles con la lógica de la regla.

La validación forma parte de un escenario compuesto por **tres pruebas controladas**. La primera estableció la telemetría base, la segunda confirmó la detección nativa y la tercera evaluó repetibilidad y contexto mediante Threat Hunting.

---

## Relación con las tres pruebas

| Prueba | Propósito | Resultado |
|---|---|---|
| **Prueba 1 — Telemetría base** | Confirmar Sysmon y Wazuh con PowerShell iniciado desde `cmd.exe` | Evento recibido; no corresponde al evento que activa 92057 |
| **Prueba 2 — Detection Validation** | Generar la relación `powershell.exe → powershell.exe -EncodedCommand ...` | **Rule 92057 activada correctamente** |
| **Prueba 3 — Repetibilidad / Hunting** | Repetir búsquedas y correlacionar actividad | 3 eventos con `EncodedCommand`; 1 alerta 92057 |

Esta separación evita atribuir a una sola ejecución evidencias que pertenecen a pruebas distintas.

---

## Objetivo

Validar la regla nativa **92057** comprobando que:

- Sysmon registre el **Process Create**;
- Wazuh reciba la telemetría;
- el evento sea clasificado dentro del grupo `sysmon_event1`;
- el proceso padre sea `powershell.exe`;
- la línea de comandos del proceso hijo contenga PowerShell con `-EncodedCommand` o una abreviación admitida;
- la regla **92057** genere la alerta esperada;
- no sea necesario duplicar esta detección mediante una regla personalizada.

---

## Escenario

La prueba de detección se diseñó para cumplir explícitamente la relación requerida por la regla:

```text
powershell.exe
      │
      ▼
powershell.exe -EncodedCommand QQA=
```

Comando de referencia utilizado dentro del escenario:

```powershell
powershell.exe -EncodedCommand QQA=
```

`QQA=` es Base64 válido y, interpretado como UTF-16LE, representa `A`. El objetivo del laboratorio no fue ejecutar una carga maliciosa, sino producir de manera segura la telemetría necesaria para comprobar el comportamiento del SIEM.

---

## Arquitectura de detección

```text
Windows 11
    │
    ▼
Sysmon Event ID 1
    │
    ▼
Wazuh Agent
    │
    ▼
Wazuh Manager / Analysis Engine
    │
    ▼
Group: sysmon_event1
    │
    ▼
Rule 92057
    │
    ▼
Security Alert
```

---

## Tecnologías utilizadas

- Wazuh 4.14.5.
- Windows 11.
- Sysmon.
- PowerShell.
- Wazuh Dashboard.

---

## Evidencia validada

La validación se apoyó en tres conjuntos de evidencia:

1. **Telemetría base:** una ejecución con `cmd.exe` como proceso padre, utilizada para comprobar la captura del campo `CommandLine`.
2. **Evento de detección:** una ejecución PowerShell cuyo proceso padre también fue `powershell.exe`, condición necesaria para la regla 92057.
3. **Búsqueda de contexto:** consultas posteriores que identificaron tres eventos relacionados con `EncodedCommand` y una alerta específica `rule.id:92057`.

La evidencia de la primera prueba no debe utilizarse como si fuera el evento exacto que activó la regla.

---

## Definición técnica de la regla

En Wazuh 4.14.5 la regla se encuentra en el ruleset oficial para Sysmon Event ID 1 y utiliza la siguiente lógica relevante:

```xml
<rule id="92057" level="12">
    <if_group>sysmon_event1</if_group>
    <field name="win.eventdata.parentImage" type="pcre2">(?i)powershell\.exe</field>
    <field name="win.eventdata.commandLine" type="pcre2">(?i)powershell\.exe.+\-\b(encodedcommand|e|ea|ec|encodeda|encode|en|enco)\b</field>
    <options>no_full_log</options>
    <description>Powershell.exe spawned a powershell process which executed a base64 encoded command</description>
    <mitre>
        <id>T1059.001</id>
    </mitre>
</rule>
```

### Condiciones principales

- El evento debe pertenecer a `sysmon_event1`.
- `parentImage` debe corresponder a `powershell.exe`.
- `commandLine` debe contener una nueva ejecución de PowerShell con `-EncodedCommand` o una abreviación contemplada por la expresión regular.

---

## Flujo de validación

```text
Sysmon Event ID 1
        │
        ▼
Clasificación sysmon_event1
        │
        ▼
Parent Image = powershell.exe
        │
        ▼
CommandLine = powershell.exe ... -EncodedCommand ...
        │
        ▼
Rule 92057
        │
        ▼
Alert Generated
```

---

## Resultado

La prueba confirmó que:

- Sysmon registró el evento requerido.
- Wazuh procesó la telemetría correctamente.
- La regla nativa **92057** se activó cuando se cumplieron sus condiciones.
- La regla tiene nivel **12** en Wazuh 4.14.5.
- No es necesario crear una regla personalizada para reproducir esta misma lógica.

---

## Análisis técnico

La validación demuestra un principio importante de **Detection Engineering**: antes de desarrollar contenido personalizado, debe comprobarse si el SIEM ya dispone de una detección nativa adecuada.

También demuestra por qué la correlación precisa de evidencia es importante. Una búsqueda por `EncodedCommand` puede devolver varias ejecuciones, pero una regla puede activarse solo sobre aquellas que cumplen todas sus condiciones, incluyendo la relación entre proceso padre e hijo.

---

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| Execution | **T1059.001 — PowerShell** |
| Defense Evasion / contexto de ofuscación | **T1027.010 — Command Obfuscation** |

La regla Wazuh 92057 está mapeada directamente a T1059.001. T1027.010 se utiliza aquí únicamente como contexto analítico del uso de contenido codificado u ofuscado.

---

## Lecciones aprendidas

- La evidencia de distintas pruebas no debe mezclarse como si correspondiera a una única ejecución.
- La lógica completa de una regla debe validarse antes de atribuirle una alerta.
- Sysmon Event ID 1 proporciona telemetría de alta calidad para análisis de procesos.
- La relación **parent-child process** es determinante en muchas detecciones.
- La validación de reglas nativas debe preceder al desarrollo de detecciones personalizadas.

---

## Conclusión

La validación confirmó que **Wazuh 4.14.5 Rule 92057** proporciona cobertura nativa para el escenario específico en que PowerShell inicia otro proceso PowerShell utilizando `-EncodedCommand` o una variante contemplada por la regla.

El escenario completo queda documentado de forma coherente mediante tres pruebas: telemetría base, Detection Validation y Threat Hunting. De esta forma, cada evidencia conserva su contexto y puede relacionarse correctamente con las demás.

---

## Proyectos relacionados

- **WI-001** — PowerShell EncodedCommand.
- **TH-001** — Threat Hunting: PowerShell EncodedCommand.
- **CS-001** — PowerShell EncodedCommand Investigation.
