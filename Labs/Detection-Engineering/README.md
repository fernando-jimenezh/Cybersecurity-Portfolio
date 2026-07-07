# Detection Engineering

## Objetivo

Diseñar, implementar y validar reglas de detección orientadas a identificar actividades potencialmente maliciosas utilizando **Wazuh SIEM**, reglas personalizadas y el framework **MITRE ATT&CK**, con el propósito de mejorar la capacidad de detección del laboratorio.

---

# Alcance

Este laboratorio contempla el desarrollo y validación de mecanismos de detección basados en la telemetría recopilada por el laboratorio.

Incluye:

- Análisis de eventos.
- Diseño de reglas.
- Validación de alertas.
- Optimización de detecciones.
- Reducción de falsos positivos.
- Documentación técnica.

No contempla actividades de respuesta a incidentes, las cuales serán desarrolladas en el laboratorio **Incident Response**.

---

# Arquitectura

```
Endpoints
│
├── Windows 11
└── Ubuntu
        │
        ▼
   Wazuh Agent
        │
        ▼
  Wazuh Manager
        │
        ▼
 Analysis Engine
        │
        ▼
 Detection Rules
        │
        ▼
 Alert Generation
        │
        ▼
Wazuh Dashboard
```

---

# Tecnologías Utilizadas

## SIEM

- Wazuh

## Sistemas Operativos

- Windows 11
- Ubuntu

## Herramientas

- Sysmon
- Sigma
- PowerShell
- XML
- JSON

## Framework

- MITRE ATT&CK

---

# Requisitos

Antes de iniciar este laboratorio se verificó:

- Recepción correcta de telemetría.
- Funcionamiento del Manager.
- Agentes activos.
- Dashboard operativo.
- Eventos disponibles para análisis.

---

# Implementación

Las principales actividades realizadas fueron:

1. Identificación de eventos relevantes.
2. Análisis de la telemetría.
3. Diseño de reglas de detección.
4. Validación de reglas.
5. Ajuste de condiciones.
6. Optimización de alertas.
7. Documentación de resultados.

---

# Configuración

Las reglas desarrolladas consideran:

- Nivel de severidad.
- Fuente del evento.
- Condiciones de coincidencia.
- Campos relevantes.
- Contexto del evento.
- Clasificación de la alerta.

Las configuraciones específicas serán documentadas dentro de los proyectos correspondientes.

---

# Validación

Cada regla es validada verificando:

- Activación correcta.
- Calidad de la alerta.
- Información proporcionada.
- Nivel de severidad.
- Reducción de falsos positivos.
- Repetibilidad de la detección.

---

# Evidencias

Las evidencias podrán incluir:

- Eventos utilizados.
- Reglas implementadas.
- Alertas generadas.
- Capturas del Dashboard.
- Resultados obtenidos.

---

# Detecciones Implementadas

Durante este laboratorio se desarrollarán detecciones para escenarios como:

- Ejecución de PowerShell.
- Uso de LOLBins.
- Creación de procesos.
- Persistencia.
- Cambios en el Registro.
- Creación de servicios.
- Tareas programadas.
- Actividad administrativa inusual.

Cada caso será documentado de forma independiente.

---

# Mapeo MITRE ATT&CK

Cada regla será relacionada con la técnica correspondiente del framework **MITRE ATT&CK**, facilitando la comprensión del comportamiento detectado y la cobertura del laboratorio.

---

# Aplicación en un Entorno Empresarial

Las actividades realizadas representan funciones habituales de un **Detection Engineer** y de un **SOC Analyst**, entre ellas:

- Desarrollo de reglas de detección.
- Validación de alertas.
- Optimización de casos de uso.
- Reducción de falsos positivos.
- Mejora continua de la capacidad de detección.

---

# Competencias Desarrolladas

Al finalizar este laboratorio se fortalecieron las siguientes competencias:

- Detection Engineering.
- Desarrollo de reglas para Wazuh.
- Interpretación de eventos.
- Correlación de información.
- MITRE ATT&CK.
- Optimización de alertas.
- Documentación técnica.

---

# Lecciones Aprendidas

- Una buena detección comienza con una adecuada comprensión de la telemetría.
- La validación continua mejora la calidad de las alertas.
- Reducir falsos positivos incrementa la eficiencia operativa del SOC.
- Las reglas deben mantenerse y ajustarse de forma continua para responder a nuevas amenazas.

---

# Referencias

- Wazuh Documentation
- Sigma Documentation
- MITRE ATT&CK
- Microsoft Learn
