# DR-003 - Detect whoami Enumeration

## Executive Summary

Durante la revisión del ruleset nativo de Wazuh se evaluó la capacidad de detección para la ejecución de **whoami.exe**, un comando nativo de Windows ampliamente utilizado durante la fase de reconocimiento (Discovery).

La investigación confirmó que, aunque Wazuh implementa cobertura para la técnica **MITRE ATT&CK T1033 (System Owner/User Discovery)** en escenarios específicos, no existe una regla nativa que detecte la ejecución de **whoami.exe** registrada por Sysmon Event ID 1.

Como resultado, se diseñó e implementó una regla personalizada para complementar la cobertura de detección del SIEM.

---

# Objective

Validar si Wazuh detecta de forma nativa la ejecución de **whoami.exe** y, en caso contrario, desarrollar una regla personalizada para cubrir esta brecha de detección.

---

# Scenario

Durante el laboratorio se ejecutó el siguiente comando desde una consola CMD:

```cmd
whoami
```

La ejecución fue registrada por Sysmon como **Process Create (Event ID 1)** y posteriormente enviada a Wazuh para su análisis.

---

# Environment

| Component | Value |
|-----------|-------|
| Operating System | Windows 11 |
| SIEM | Wazuh 4.14.5 |
| Telemetry | Sysmon |
| Hypervisor | VirtualBox |

---

# Evidence

## Command Executed

```cmd
whoami
```

## Sysmon Event

| Field | Value |
|--------|-------|
| Event ID | 1 |
| Image | C:\Windows\System32\whoami.exe |
| Parent Image | C:\Windows\System32\cmd.exe |
| Command Line | whoami |
| User | DESKTOP-7CLFI8R\lab |
| Integrity Level | High |

---

# Native Rule Analysis

Como parte de la investigación se revisó el ruleset oficial de Wazuh utilizando búsquedas directas sobre los archivos de reglas.

Se confirmó que:

- No existe una regla específica para **whoami.exe**.
- La técnica **T1033** sí está implementada para otros escenarios.
- Las reglas existentes están orientadas a herramientas como **qwinsta** y determinadas actividades realizadas desde PowerShell.

La evidencia permitió concluir que la ejecución de **whoami.exe** mediante Sysmon Event ID 1 no genera una alerta nativa.

---

# Detection Gap

La investigación identificó una brecha de detección:

- Sysmon registra correctamente la ejecución.
- Wazuh recibe el evento.
- El evento queda almacenado en los índices.
- No se genera una alerta específica para **whoami.exe**.

Esta situación justifica la implementación de una regla personalizada para mejorar la visibilidad sobre actividades de Discovery.

---

# Custom Rule Design

Se desarrolló una regla personalizada orientada a detectar la ejecución de **whoami.exe** iniciada desde **cmd.exe**.

La regla considera:

- Imagen ejecutada.
- Proceso padre.
- Telemetría de Sysmon Event ID 1.
- Clasificación MITRE ATT&CK.

---

# Validation

La regla personalizada fue incorporada al entorno de laboratorio y validada mediante una nueva ejecución controlada del comando:

```cmd
whoami
```

Durante la validación se comprobó que:

- La regla fue cargada correctamente por Wazuh.
- Sysmon registró nuevamente el evento.
- Wazuh generó la alerta correspondiente.
- La técnica fue clasificada como **MITRE ATT&CK T1033 – System Owner/User Discovery**.

La validación confirmó que la regla complementa la cobertura nativa del SIEM para este escenario.

---

# Results

La validación permitió confirmar que:

- Sysmon registró correctamente la ejecución.
- Wazuh recibió el evento.
- No existe una regla nativa específica para whoami.exe.
- La regla personalizada permitió detectar exitosamente la actividad.
- Se amplió la cobertura para actividades de Discovery.

---

# Technical Analysis

Aunque **whoami.exe** es una herramienta administrativa legítima, también es utilizada frecuentemente por atacantes durante la fase inicial de reconocimiento para identificar el usuario actualmente autenticado.

Por sí sola no constituye evidencia de compromiso; sin embargo, su ejecución adquiere relevancia cuando se correlaciona con otros comandos de reconocimiento como:

- hostname
- ipconfig
- systeminfo
- net user
- tasklist

La incorporación de una regla personalizada permite aumentar la visibilidad sobre este tipo de actividades y facilita investigaciones posteriores.

---

# MITRE ATT&CK

| Tactic | Technique |
|----------|-----------|
| Discovery | T1033 – System Owner/User Discovery |

---

# Lessons Learned

- No todas las técnicas MITRE cuentan con cobertura completa en el ruleset nativo.
- La revisión del contenido oficial permite identificar brechas de detección.
- Sysmon proporciona la telemetría necesaria para desarrollar reglas de alta calidad.
- Detection Engineering consiste tanto en crear nuevas reglas como en validar las capacidades existentes.
- Las reglas personalizadas permiten adaptar el SIEM a los requerimientos específicos del entorno.

---

# Conclusion

La investigación confirmó que la ejecución de **whoami.exe** no genera una detección específica dentro del ruleset nativo de Wazuh, a pesar de corresponder a una técnica de Discovery ampliamente utilizada.

La implementación de una regla personalizada permitió complementar esta cobertura y mejorar la capacidad de detección del laboratorio.

Este proyecto reforzó conocimientos relacionados con Detection Engineering, análisis del ruleset oficial, identificación de brechas de detección y desarrollo de contenido personalizado para Wazuh.

---

# References

- Microsoft Sysmon
- Wazuh Ruleset
- MITRE ATT&CK – T1033

---

# Related Projects

- WI-003 – whoami Enumeration
- TH-003 – Windows Discovery Commands
- CS-003 – Windows Discovery Investigation
