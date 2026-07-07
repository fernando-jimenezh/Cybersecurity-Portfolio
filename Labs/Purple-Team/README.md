# Purple Team

## Objetivo

Validar la capacidad de detección del laboratorio mediante la simulación controlada de técnicas utilizadas por actores maliciosos, verificando la efectividad de las reglas implementadas, la calidad de la telemetría y la visibilidad proporcionada por **Wazuh SIEM**.

---

# Alcance

Este laboratorio documenta las actividades realizadas para evaluar los controles de seguridad implementados dentro del laboratorio.

Incluye:

- Simulación de técnicas adversarias.
- Generación controlada de eventos.
- Validación de alertas.
- Evaluación de la capacidad de detección.
- Identificación de oportunidades de mejora.
- Documentación de resultados.

No contempla pruebas de intrusión sobre entornos de producción.

---

# Arquitectura

```
Kali Linux
      │
      ▼
Simulación Controlada
      │
      ▼
Windows / Ubuntu
      │
      ▼
Wazuh Agent
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
Análisis y Validación
```

---

# Tecnologías Utilizadas

## SIEM

- Wazuh

## Sistemas Operativos

- Windows 11
- Ubuntu
- Kali Linux

## Herramientas

- Sysmon
- PowerShell
- Bash
- Wazuh Agent

## Framework

- MITRE ATT&CK

---

# Requisitos

Antes de iniciar las simulaciones se verificó:

- Funcionamiento del laboratorio.
- Disponibilidad de la telemetría.
- Estado operativo del SIEM.
- Agentes activos.
- Comunicación entre todos los componentes.

---

# Implementación

Las actividades desarrolladas incluyen:

1. Definición del escenario.
2. Selección de la técnica a validar.
3. Ejecución controlada.
4. Generación de eventos.
5. Recepción de la telemetría.
6. Validación de alertas.
7. Documentación de resultados.

---

# Configuración

Las validaciones utilizan la información obtenida desde:

- Windows Event Logs.
- Sysmon.
- auditd.
- Wazuh SIEM.
- Dashboard.

Las configuraciones específicas de cada simulación serán documentadas en los proyectos correspondientes.

---

# Validación

Cada ejercicio contempla:

- Confirmación de la ejecución.
- Recepción de eventos.
- Activación de alertas.
- Correlación de información.
- Evaluación de la detección.
- Documentación de resultados.

---

# Evidencias

Las actividades podrán documentar:

- Eventos generados.
- Alertas recibidas.
- Procesos ejecutados.
- Línea de tiempo.
- Hallazgos obtenidos.
- Observaciones técnicas.

---

# Detecciones Implementadas

Las simulaciones permiten validar:

- Reglas predeterminadas de Wazuh.
- Reglas personalizadas.
- Calidad de la telemetría.
- Cobertura de las detecciones implementadas.

---

# Mapeo MITRE ATT&CK

Cada escenario será relacionado con las tácticas y técnicas correspondientes del framework **MITRE ATT&CK**, permitiendo evaluar la cobertura del laboratorio y detectar oportunidades de mejora.

---

# Aplicación en un Entorno Empresarial

Las actividades desarrolladas representan tareas habituales realizadas por equipos **Purple Team**, permitiendo:

- Validar controles de seguridad.
- Evaluar la capacidad de detección.
- Medir la efectividad de las reglas implementadas.
- Identificar brechas de visibilidad.
- Mejorar continuamente los procesos de monitoreo.

---

# Competencias Desarrolladas

Al finalizar este laboratorio se fortalecieron las siguientes competencias:

- Purple Team.
- Validación de controles de seguridad.
- Simulación de escenarios.
- Evaluación de reglas de detección.
- Correlación de eventos.
- MITRE ATT&CK.
- Documentación técnica.

---

# Lecciones Aprendidas

- La simulación controlada permite evaluar objetivamente la capacidad de detección del laboratorio.
- La calidad de la telemetría influye directamente en la efectividad del monitoreo.
- La validación continua mejora la cobertura de las reglas de detección.
- La documentación de cada ejercicio facilita la mejora continua del entorno.

---

# Referencias

- MITRE ATT&CK
- Wazuh Documentation
- Microsoft Learn
- Red Canary Atomic Red Team
