# DR-001 - Validate Wazuh Rule 92057 - PowerShell EncodedCommand

## Objetivo

Validar el funcionamiento de la regla nativa **92057** de Wazuh para detectar la ejecución de PowerShell utilizando el parámetro **-EncodedCommand**, verificando la generación de telemetría, el procesamiento del evento y la activación de la detección.

---

# Escenario

Durante una investigación realizada en el laboratorio (WI-001), se ejecutó PowerShell utilizando el parámetro **-EncodedCommand** para generar telemetría controlada y validar las capacidades de detección del SIEM.

Comando ejecutado:

```powershell
powershell.exe -EncodedCommand QQA=
```

Aunque el comando genera un error debido al contenido Base64 inválido, la ejecución es suficiente para producir la telemetría necesaria para el análisis.

---

# Objetivo de la Validación

Confirmar que:

- Sysmon registra correctamente el evento.
- Wazuh recibe la telemetría.
- El evento es procesado por el motor de reglas.
- Existe una detección nativa para este comportamiento.
- No es necesario desarrollar una regla personalizada para este caso de uso.

---

# Arquitectura

```
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
Motor de Reglas
      │
      ▼
Regla 92057
      │
      ▼
Alerta
```

---

# Tecnologías Utilizadas

- Wazuh 4.14.5
- Windows 11
- Sysmon
- PowerShell
- Wazuh Dashboard

---

# Evidencia Analizada

Durante la validación se identificó el siguiente evento:

| Campo | Valor |
|--------|-------|
| Provider | Microsoft-Windows-Sysmon |
| Event ID | 1 |
| Image | powershell.exe |
| Parent Image | cmd.exe |
| CommandLine | powershell.exe -EncodedCommand QQA= |

El evento fue recibido correctamente por Wazuh y almacenado en los índices correspondientes.

---

# Investigación del Motor de Reglas

Como parte de la validación se analizó el funcionamiento interno del motor de reglas de Wazuh.

Se verificó la cadena de procesamiento del evento:

```
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
0800-sysmon_id_1.xml
        │
        ▼
Reglas de Detección
```

Durante el análisis se inspeccionaron los siguientes archivos del ruleset oficial:

- 0330-sysmon_rules.xml
- 0800-sysmon_id_1.xml

Esto permitió comprender cómo Wazuh clasifica inicialmente los eventos de Sysmon antes de aplicar reglas de detección más específicas.

---

# Regla Detectada

Durante la investigación se confirmó que Wazuh incluye una regla nativa capaz de detectar este comportamiento.

**Rule ID**

```
92057
```

**Descripción**

```
Powershell.exe spawned a powershell process which executed a base64 encoded command
```

Esta regla fue activada automáticamente al procesar el evento generado durante el laboratorio.

---

# Resultado

La investigación permitió validar que:

- La telemetría fue generada correctamente.
- Sysmon registró el Event ID 1.
- Wazuh recibió el evento.
- El motor de reglas clasificó correctamente la actividad.
- La regla nativa 92057 detectó exitosamente el comportamiento.

No fue necesario desarrollar una regla personalizada para este caso de uso.

---

# Análisis

Este laboratorio demuestra la importancia de validar las capacidades nativas del SIEM antes de desarrollar contenido personalizado.

La revisión del ruleset oficial confirmó que Wazuh ya incorpora cobertura para esta técnica, evitando la creación de reglas duplicadas y reduciendo el esfuerzo de mantenimiento.

Asimismo, el análisis permitió comprender la relación existente entre las reglas base, los grupos utilizados durante la correlación y las reglas finales de detección.

---

# Lecciones Aprendidas

- No toda técnica requiere una regla personalizada.
- Es recomendable revisar el contenido nativo del SIEM antes de crear nuevas detecciones.
- Comprender la cadena de procesamiento de eventos facilita el desarrollo y la validación de reglas.
- Sysmon proporciona una fuente de telemetría altamente útil para Detection Engineering.
- Wazuh permite validar el comportamiento de sus reglas mediante herramientas como **wazuh-logtest**.

---

# MITRE ATT&CK

| Táctica | Técnica |
|----------|----------|
| Execution | T1059.001 - PowerShell |

---

# Conclusión

La validación confirmó que Wazuh proporciona cobertura nativa para la detección de PowerShell ejecutado mediante **-EncodedCommand**.

El laboratorio permitió comprender el flujo completo del evento, desde la generación de la telemetría hasta la activación de la regla oficial, reforzando conocimientos relacionados con Detection Engineering, análisis del motor de reglas y validación de capacidades de detección dentro de Wazuh.
