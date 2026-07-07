# Foundation - Telemetry Collection

## Objetivo

Implementar la recolección de telemetría desde los diferentes sistemas del laboratorio hacia la plataforma **Wazuh SIEM**, garantizando la disponibilidad de eventos necesarios para las actividades de **Security Monitoring**, **Threat Hunting**, **Detection Engineering** e **Incident Response**.

---

# Alcance

Este laboratorio contempla la incorporación de los endpoints al SIEM y la validación de la generación de eventos de seguridad.

Incluye:

- Registro de agentes Wazuh.
- Configuración de Windows.
- Configuración de Linux.
- Validación de conectividad.
- Recepción de eventos.
- Verificación de telemetría.

No contempla la creación de reglas de detección ni el análisis de amenazas, actividades que serán desarrolladas en laboratorios posteriores.

---

# Arquitectura

La recolección de eventos se realiza desde los endpoints hacia el servidor Wazuh mediante agentes instalados en cada sistema operativo.

```
                     Wazuh Dashboard
                            │
                            ▼
                    Wazuh Manager
                            │
                            ▼
                    Wazuh Indexer
                     ▲            ▲
                     │            │
             Windows Agent   Linux Agent
```

Cada endpoint genera eventos que son enviados al Manager para su análisis y posterior almacenamiento en el Indexer.

---

# Tecnologías Utilizadas

## SIEM

- Wazuh

## Sistemas Operativos

- Windows 11
- Ubuntu

## Agentes

- Wazuh Agent

## Telemetría

### Windows

- Windows Event Logs
- Sysmon

### Linux

- auditd
- Syslog
- Journalctl

---

# Requisitos

Antes de iniciar este laboratorio se verificó:

- Wazuh Manager operativo.
- Wazuh Dashboard accesible.
- Comunicación entre equipos.
- Resolución DNS.
- Conectividad de red.

---

# Implementación

Las principales actividades fueron:

1. Instalación del agente Wazuh en Windows.
2. Instalación del agente Wazuh en Ubuntu.
3. Registro de agentes.
4. Configuración del archivo `ossec.conf`.
5. Reinicio de servicios.
6. Validación de comunicación con el Manager.
7. Confirmación del estado de los agentes.

---

# Configuración

## Windows

Se configuró:

- Wazuh Agent.
- Windows Event Logs.
- Sysmon.

Se verificó la correcta transmisión de eventos hacia el servidor.

---

## Ubuntu

Se configuró:

- Wazuh Agent.
- auditd.
- Syslog.
- Journalctl.

Posteriormente se validó la recepción de eventos desde Linux.

---

# Flujo de Telemetría

El proceso de recolección de eventos sigue el siguiente flujo:

```
Evento generado
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
Indexer
        │
        ▼
Dashboard
```

Este flujo permite transformar eventos del sistema operativo en alertas disponibles para análisis e investigación.

---

# Validación

Se verificó:

- Agentes conectados.
- Último Keep Alive.
- Estado Active.
- Recepción de eventos.
- Visualización desde el Dashboard.
- Comunicación continua con el Manager.

---

# Problemas Encontrados

Durante la implementación pueden presentarse situaciones como:

- Agentes desconectados.
- Configuración incorrecta del Manager.
- Errores en certificados.
- Bloqueo por Firewall.
- Desincronización horaria.
- Errores de configuración del agente.

Cada incidencia fue documentada y corregida antes de continuar con el laboratorio.

---

# Solución Aplicada

Las validaciones realizadas incluyeron:

- Revisión del archivo `ossec.conf`.
- Verificación de servicios.
- Validación mediante logs.
- Reinicio del agente.
- Comprobación de conectividad.
- Verificación desde el Dashboard.

---

# Evidencias

Este laboratorio documenta:

- Registro de agentes.
- Estado de conexión.
- Capturas del Dashboard.
- Configuración del agente.
- Eventos recibidos.
- Estado de sincronización.

Las evidencias serán incorporadas durante el desarrollo del laboratorio.

---

# Detecciones Implementadas

No aplica.

En este laboratorio únicamente se valida la correcta generación y recepción de telemetría.

Las primeras reglas serán desarrolladas en **Detection Engineering**.

---

# Mapeo MITRE ATT&CK

No aplica.

Este laboratorio corresponde a la implementación de la infraestructura de monitoreo.

---

# Lecciones Aprendidas

- La calidad del monitoreo depende directamente de la calidad de la telemetría.
- Una configuración adecuada del agente facilita las investigaciones posteriores.
- La validación continua de la conectividad evita pérdida de eventos.
- La generación de eventos es la base para cualquier actividad de Threat Hunting o Incident Response.

---

# Referencias

- Wazuh Documentation
- Sysmon Documentation
- Microsoft Learn
- Linux auditd Documentation
