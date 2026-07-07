# Detection Rules

## Descripción

La carpeta **Detection Rules** reúne las reglas de detección desarrolladas y validadas durante la operación del laboratorio de ciberseguridad.

Cada regla documenta el proceso seguido para detectar una técnica, comportamiento o actividad específica utilizando **Wazuh SIEM** como plataforma principal de monitoreo.

El propósito de esta sección es demostrar la capacidad para diseñar, validar y mejorar mecanismos de detección basados en la telemetría disponible y alineados con el framework **MITRE ATT&CK**.

---

# Objetivos

Esta sección tiene como finalidad:

- Desarrollar reglas de detección para escenarios reales.
- Validar el funcionamiento de las reglas implementadas.
- Reducir falsos positivos.
- Mejorar la visibilidad sobre eventos de seguridad.
- Documentar el proceso de desarrollo y validación.
- Mantener un repositorio de reglas reutilizables.

---

# Alcance

Las reglas desarrolladas podrán orientarse a detectar actividades relacionadas con:

- PowerShell.
- CMD.
- LOLBins.
- Sysmon.
- Windows Event Logs.
- auditd.
- Persistencia.
- Escalamiento de privilegios.
- Credential Access.
- Defense Evasion.
- Creación de procesos.
- Cambios en servicios del sistema.
- Tareas programadas.
- Actividad administrativa inusual.

Cada regla será documentada de forma independiente.

---

# Metodología

Todas las reglas seguirán una metodología uniforme que facilite su desarrollo, validación y mantenimiento.

## Estructura

Cada regla incluirá como mínimo:

- Objetivo.
- Escenario.
- Fuente de información.
- Lógica de detección.
- Validación.
- Resultado.
- Mapeo MITRE ATT&CK.
- Competencias Desarrolladas.
- Lecciones Aprendidas.

---

# Tecnologías Utilizadas

Las reglas podrán utilizar información proveniente de:

- Wazuh SIEM.
- Sysmon.
- Windows Event Logs.
- auditd.
- Sigma.
- MITRE ATT&CK.

---

# Validación

Cada regla será validada mediante pruebas realizadas dentro del laboratorio.

Las validaciones permitirán comprobar:

- Activación de la regla.
- Calidad de la alerta.
- Contexto del evento.
- Nivel de severidad.
- Precisión de la detección.
- Reducción de falsos positivos.

---

# Tipos de Reglas

Algunos ejemplos de reglas que formarán parte de esta sección son:

- Detección de ejecución de PowerShell.
- Uso de LOLBins.
- Creación de procesos sospechosos.
- Persistencia mediante tareas programadas.
- Creación de nuevos servicios.
- Cambios en el Registro de Windows.
- Actividad administrativa inusual.
- Intentos de escalamiento de privilegios.
- Autenticaciones sospechosas.

Cada regla será desarrollada y documentada de forma independiente.

---

# Objetivo del Portafolio

Las reglas documentadas en esta sección representan la evolución de las capacidades de detección implementadas durante el desarrollo del laboratorio, demostrando experiencia en el diseño, validación y mejora continua de mecanismos de detección para entornos **Blue Team**.
