# CS-003 - Windows Discovery Investigation

## Executive Summary

Durante las actividades de monitoreo del laboratorio se identificó la ejecución del comando nativo **whoami.exe**, utilizado para obtener información sobre el usuario actualmente autenticado.

Aunque esta herramienta forma parte de la administración normal de Windows, también es ampliamente utilizada durante la fase de reconocimiento por atacantes para recopilar información del entorno antes de ejecutar acciones posteriores.

La investigación permitió validar la telemetría generada por Sysmon, confirmar la recepción del evento por Wazuh, identificar una brecha en el ruleset nativo para este escenario específico y desarrollar una regla personalizada que mejora la capacidad de detección del SIEM.

Finalmente se realizó una actividad de Threat Hunting para determinar si la ejecución observada correspondía a un evento aislado o formaba parte de una secuencia más amplia de actividades de reconocimiento.

---

# Objective

Investigar la ejecución de **whoami.exe**, validar el flujo completo de detección dentro de Wazuh, analizar la cobertura del ruleset oficial y determinar si la actividad corresponde a un comportamiento aislado o a una posible fase de Discovery.

---

# Environment

| Component | Value |
|-----------|-------|
| Operating System | Windows 11 |
| SIEM | Wazuh 4.14.5 |
| Telemetry | Sysmon |
| Hypervisor | VirtualBox |

---

# Scenario

Como parte del laboratorio se ejecutó una prueba controlada utilizando el comando nativo de Windows:

```cmd
whoami
```

El objetivo fue generar telemetría relacionada con actividades de reconocimiento y evaluar la capacidad de detección del SIEM.

---

# Scope

La investigación incluyó:

- Generación de telemetría.
- Registro del evento mediante Sysmon.
- Recepción del evento por Wazuh.
- Revisión del ruleset oficial.
- Identificación de cobertura nativa.
- Diseño de una regla personalizada.
- Actividad de Threat Hunting.
- Documentación del caso.

---

# Investigation

La investigación comenzó tras identificar la ejecución de **whoami.exe** registrada por Sysmon Event ID 1.

Se verificó que el evento fue recibido correctamente por Wazuh y almacenado dentro de los índices correspondientes.

Posteriormente se revisó el ruleset oficial para determinar si existía una regla específica para detectar este comportamiento.

La revisión confirmó que Wazuh implementa cobertura para la técnica **MITRE ATT&CK T1033** únicamente en determinados escenarios, sin incluir la ejecución de **whoami.exe**.

Como resultado, se diseñó una regla personalizada para complementar la cobertura de detección.

Finalmente se realizó una actividad de Threat Hunting con el objetivo de identificar otras ejecuciones de comandos de Discovery dentro del entorno monitoreado.

---

# Timeline

| Time | Event |
|------|-------|
| 20:42:18 | Ejecución de whoami.exe |
| 20:42:18 | Sysmon registra Event ID 1 |
| Posteriormente | Wazuh recibe el evento |
| Posteriormente | Revisión del ruleset oficial |
| Posteriormente | Diseño de regla personalizada |
| Posteriormente | Actividad de Threat Hunting |
| Final | Caso documentado |

---

# Evidence

## Process Execution

| Field | Value |
|--------|-------|
| Event ID | 1 |
| Image | C:\Windows\System32\whoami.exe |
| Parent Image | C:\Windows\System32\cmd.exe |
| Command Line | whoami |
| User | DESKTOP-7CLFI8R\lab |
| Integrity Level | High |

---

## Rule Analysis

Durante la revisión del ruleset oficial se comprobó que:

- No existe una regla específica para **whoami.exe**.
- Existen reglas asociadas a la técnica **T1033**, pero orientadas a otros escenarios.
- Fue necesaria una regla personalizada para cubrir esta actividad.

---

# Technical Analysis

El comando **whoami.exe** forma parte de las herramientas nativas de administración de Windows.

Sin embargo, también es utilizado frecuentemente por actores maliciosos durante la fase de reconocimiento para identificar el contexto del usuario comprometido.

Durante la investigación se confirmó que:

- El proceso fue iniciado desde **cmd.exe**.
- La ejecución ocurrió bajo el usuario del laboratorio.
- Sysmon registró correctamente toda la información necesaria para reconstruir el evento.
- Wazuh almacenó la telemetría sin generar una alerta nativa específica.

La ausencia de una regla dedicada justificó el desarrollo de contenido personalizado para Detection Engineering.

---

# Detection Validation

Como parte del caso de estudio se revisó el contenido del ruleset oficial de Wazuh.

La investigación confirmó que:

- El evento fue procesado correctamente.
- No existe una regla nativa específica para **whoami.exe**.
- La cobertura para **MITRE T1033** es parcial.
- La regla personalizada permitió complementar la capacidad de detección del SIEM.

---

# Threat Hunting Assessment

La actividad de Threat Hunting permitió determinar que:

- Solo se observó una ejecución de **whoami.exe**.
- No se identificaron otros comandos de Discovery ejecutados durante el mismo período.
- No existieron evidencias de movimiento lateral.
- No se identificaron mecanismos de persistencia.
- La actividad permaneció limitada al entorno del laboratorio.

La evidencia disponible permitió clasificar el evento como una ejecución aislada correspondiente a una prueba controlada.

---

# Risk Assessment

| Factor | Assessment |
|---------|------------|
| Probability | Low |
| Impact | Low |
| Priority | Low |

Aunque **whoami.exe** es una herramienta legítima, su ejecución debe analizarse dentro del contexto general de la actividad observada.

---

# MITRE ATT&CK

| Tactic | Technique |
|----------|-----------|
| Discovery | T1033 – System Owner/User Discovery |

---

# Recommendations

- Correlacionar whoami con otros comandos de Discovery.
- Revisar procesos padre e hijos.
- Validar el contexto del usuario ejecutor.
- Correlacionar eventos Sysmon adicionales.
- Mantener reglas personalizadas para complementar la cobertura del SIEM.

---

# Lessons Learned

- No todas las técnicas MITRE cuentan con cobertura completa dentro del ruleset nativo.
- Sysmon proporciona información suficiente para reconstruir la actividad de reconocimiento.
- Detection Engineering permite cerrar brechas de detección mediante reglas personalizadas.
- Threat Hunting ayuda a determinar si un evento aislado forma parte de una actividad maliciosa más amplia.
- La correlación entre investigación, detección y hunting mejora significativamente la calidad del análisis.

---

# Conclusion

La investigación permitió reconstruir completamente la ejecución de **whoami.exe** dentro del laboratorio, validando la generación de telemetría mediante Sysmon y su correcta recepción por Wazuh.

Asimismo, el análisis del ruleset oficial permitió identificar una brecha de cobertura para este escenario específico, justificando el desarrollo de una regla personalizada orientada a mejorar la detección de actividades de Discovery.

Finalmente, la actividad de Threat Hunting confirmó que la ejecución correspondió a una prueba controlada y no se identificaron indicadores adicionales de compromiso.

Este caso de estudio consolidó conocimientos relacionados con investigación de eventos Windows, Detection Engineering, Threat Hunting y análisis de telemetría dentro de un entorno Blue Team.

---

# References

- Microsoft Sysmon
- Wazuh Documentation
- MITRE ATT&CK – T1033 (System Owner/User Discovery)

---

# Related Projects

- WI-003 – whoami Enumeration
- DR-003 – Detect whoami Enumeration
- TH-003 – Windows Discovery Commands
