# TH-003 - Threat Hunting: Windows Discovery Commands

## Executive Summary

Durante las actividades de Threat Hunting se investigó la ejecución de comandos nativos de reconocimiento en Windows, utilizando como punto de partida la ejecución de **whoami.exe** registrada por Sysmon.

El objetivo fue determinar si la actividad observada correspondía a un evento aislado o formaba parte de una secuencia más amplia de reconocimiento dentro del entorno monitoreado.

La investigación confirmó que la actividad estuvo limitada al laboratorio y no se identificaron indicadores adicionales de compromiso.

---

# Objective

Realizar una actividad de Threat Hunting sobre comandos de reconocimiento en Windows para identificar posibles patrones asociados a la fase de Discovery descrita por MITRE ATT&CK.

---

# Hunting Hypothesis

Los atacantes suelen ejecutar comandos nativos de Windows para obtener información del sistema antes de realizar acciones posteriores.

Hipótesis:

> Si un atacante ejecuta comandos de reconocimiento, deberían existir múltiples eventos relacionados con herramientas nativas como whoami, hostname, ipconfig, systeminfo, net.exe o cmd.exe.

---

# Environment

| Component | Value |
|-----------|-------|
| Operating System | Windows 11 |
| SIEM | Wazuh 4.14.5 |
| Telemetry | Sysmon |
| Hypervisor | VirtualBox |

---

# Investigation Methodology

La investigación comenzó a partir de la ejecución controlada de **whoami.exe**.

Posteriormente se realizaron búsquedas para determinar:

- Ejecuciones de whoami.
- Procesos padre asociados.
- Usuario ejecutor.
- Endpoint afectado.
- Eventos Sysmon relacionados.

---

# Hunting Queries

## whoami Executions

```kql
data.win.eventdata.image:*whoami.exe*
```

Resultado:

- 1 evento observado.

---

## Parent Process

```kql
data.win.eventdata.parentImage:*cmd.exe*
```

Resultado:

- El proceso padre identificado fue **cmd.exe**.

---

## Command Line

```kql
data.win.eventdata.commandLine:whoami
```

Resultado:

- La ejecución coincidió con el comando esperado.

---

## User

```kql
data.win.eventdata.user:*
```

Resultado:

Usuario observado:

```
DESKTOP-7CLFI8R\lab
```

---

## Endpoint

```kql
agent.name:W11-Lab
```

Resultado:

La actividad quedó limitada al equipo de laboratorio.

---

# Findings

La investigación permitió determinar que:

- Se registró una única ejecución de whoami.exe.
- La ejecución fue iniciada desde cmd.exe.
- No se identificaron múltiples comandos de reconocimiento consecutivos.
- No hubo evidencia de movimiento lateral.
- No se observaron mecanismos de persistencia.
- No se detectó actividad posterior asociada.

---

# Indicators Reviewed

## Process

```
whoami.exe
```

## Parent Process

```
cmd.exe
```

## User

```
DESKTOP-7CLFI8R\lab
```

## Endpoint

```
W11-Lab
```

---

# Threat Hunting Assessment

La actividad corresponde a una prueba controlada del laboratorio.

Aunque **whoami.exe** es una herramienta legítima de administración, también es utilizada durante la fase de reconocimiento por numerosos marcos ofensivos y actores maliciosos.

La investigación no identificó evidencia suficiente para considerar la actividad como un compromiso del sistema.

---

# MITRE ATT&CK

| Tactic | Technique |
|----------|-----------|
| Discovery | T1033 – System Owner/User Discovery |

---

# Recommendations

- Correlacionar whoami con otros comandos de reconocimiento.
- Revisar la secuencia completa de procesos padre e hijos.
- Monitorear ejecuciones repetitivas desde PowerShell o cmd.exe.
- Correlacionar con conexiones de red y eventos posteriores.
- Identificar patrones de Discovery ejecutados en un corto intervalo de tiempo.

---

# Lessons Learned

- Una única herramienta de reconocimiento rara vez constituye evidencia suficiente de un compromiso.
- Threat Hunting permite ampliar el contexto de una alerta individual.
- La correlación entre procesos aporta información valiosa para reconstruir la actividad.
- Los comandos nativos de Windows deben analizarse siempre dentro de su contexto operacional.

---

# Conclusion

La actividad de Threat Hunting confirmó que la ejecución de **whoami.exe** correspondió a una acción aislada realizada dentro del laboratorio.

No se identificaron indicadores adicionales de reconocimiento, persistencia o compromiso que justificaran elevar la criticidad del evento.

La investigación permitió validar la utilidad de Sysmon y Wazuh para identificar y contextualizar actividades de Discovery dentro de un entorno Windows.

---

# References

- Microsoft Sysmon
- MITRE ATT&CK – T1033

---

# Related Projects

- WI-003 – whoami Enumeration
- DR-003 – Detect whoami Enumeration
- CS-003 – Windows Discovery Investigation
