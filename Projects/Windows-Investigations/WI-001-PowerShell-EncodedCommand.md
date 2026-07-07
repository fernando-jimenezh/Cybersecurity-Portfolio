# WI-001 - PowerShell EncodedCommand

---

# Resumen

Se realizó una investigación sobre la ejecución de PowerShell utilizando el parámetro **-EncodedCommand**, con el objetivo de analizar la telemetría generada en el sistema operativo Windows, validar su recolección mediante Sysmon y confirmar la visualización de los eventos en Wazuh SIEM.

Esta investigación busca comprender qué información queda registrada durante la ejecución de comandos codificados y evaluar los elementos disponibles para un analista SOC durante el proceso de investigación.

---

# Objetivo

- Analizar la ejecución de PowerShell mediante **-EncodedCommand**.
- Validar la generación de eventos en Windows.
- Confirmar la recepción de la telemetría en Wazuh SIEM.
- Identificar información relevante para una investigación.
- Evaluar oportunidades de detección.

---

# Alcance

La investigación contempla el análisis de la ejecución del proceso PowerShell dentro de un laboratorio controlado.

No se evaluó la ejecución de código malicioso, únicamente la generación y análisis de la telemetría producida por el uso del parámetro **-EncodedCommand**.

---

# Entorno

| Componente | Descripción |
|------------|-------------|
| Sistema Operativo | Windows 11 |
| SIEM | Wazuh |
| Telemetría | Sysmon |
| Hipervisor | VirtualBox |

---

# Escenario

Se ejecutó PowerShell utilizando el parámetro **-EncodedCommand** con el propósito de generar eventos de telemetría para su posterior análisis.

La actividad fue realizada de forma controlada dentro del laboratorio de ciberseguridad.

---

# Procedimiento

Durante la prueba se ejecutó PowerShell utilizando un comando codificado en Base64.

Posteriormente se verificó la generación de eventos mediante Sysmon y la recepción de la información en Wazuh SIEM para su análisis.

---

# Evidencias

## Capturas

Pendiente.

---

## Eventos registrados

Pendiente.

---

## Alertas

Pendiente.

---

# Análisis

Durante la investigación se analizarán los siguientes elementos:

- Hora de ejecución.
- Usuario.
- Host.
- Image.
- ParentImage.
- CommandLine.
- ProcessId.
- Event ID.
- Rule ID.
- Nivel de severidad.
- Grupo de reglas.
- MITRE ATT&CK.

---

# Hallazgos

Pendiente de completar durante el análisis de la evidencia.

---

# Detección

Se evaluarán posibles mecanismos de detección considerando:

- CommandLine.
- Parent Process.
- Parámetros utilizados.
- Comportamiento observado.
- Correlación de eventos.

---

# MITRE ATT&CK

| Táctica | Técnica | Descripción |
|----------|----------|-------------|
| Pendiente | Pendiente | Pendiente |

---

# Conclusiones

Pendiente de completar al finalizar la investigación.

---

# Lecciones Aprendidas

Pendiente de completar una vez concluido el análisis.

---

# Estado

🟡 En desarrollo.
