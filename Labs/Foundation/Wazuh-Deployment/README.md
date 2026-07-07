# Foundation - Wazuh Deployment

## Objetivo

Implementar una plataforma **SIEM** basada en **Wazuh** que permita centralizar eventos de seguridad, administrar agentes, generar alertas y servir como plataforma principal para las actividades de **Security Monitoring**, **Threat Hunting**, **Detection Engineering** e **Incident Response**.

---

# Alcance

Este laboratorio contempla la instalación y configuración inicial de la plataforma Wazuh.

Incluye:

- Instalación del servidor.
- Configuración del SIEM.
- Instalación del Dashboard.
- Configuración del Indexer.
- Validación de servicios.
- Acceso a la interfaz web.
- Registro inicial de agentes.

No contempla la generación de telemetría, la cual será desarrollada en el laboratorio **Telemetry Collection**.

---

# Arquitectura

La plataforma fue desplegada sobre **Ubuntu Server**, utilizando una instalación distribuida por componentes.

La infraestructura quedó conformada por:

| Componente | Función |
|------------|----------|
| Wazuh Manager | Recepción y procesamiento de eventos |
| Wazuh Indexer | Almacenamiento e indexación |
| Wazuh Dashboard | Visualización y administración |
| Filebeat | Envío de eventos |
| Wazuh API | Comunicación entre servicios |

---

# Tecnologías Utilizadas

## SIEM

- Wazuh

## Sistemas Operativos

- Ubuntu Server

## Componentes

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Filebeat

---

# Requisitos

Para la implementación se consideró:

- Ubuntu Server actualizado.
- Acceso a Internet.
- Resolución DNS funcional.
- Sincronización horaria.
- Recursos suficientes para ejecutar los servicios.

---

# Implementación

Las principales actividades realizadas fueron:

1. Preparación del servidor.
2. Actualización del sistema operativo.
3. Descarga del instalador oficial.
4. Instalación de Wazuh.
5. Instalación del Indexer.
6. Instalación del Dashboard.
7. Configuración de certificados.
8. Configuración del servicio Filebeat.
9. Inicio de servicios.
10. Validación del entorno.

---

# Configuración

Durante la implementación se configuraron:

## Wazuh Manager

- Gestión de agentes.
- Recepción de eventos.
- Reglas de detección.

---

## Wazuh Indexer

Configuración del almacenamiento de eventos y comunicación segura mediante certificados.

---

## Wazuh Dashboard

Configuración del acceso web y conexión con el Indexer para la visualización de alertas.

---

## Filebeat

Configurado para el envío de eventos hacia el Indexer.

---

# Validación

Se verificó el correcto funcionamiento de:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Filebeat
- API

Se comprobó además:

- Acceso a la interfaz web.
- Estado de los servicios.
- Comunicación entre componentes.
- Recepción de eventos.

---

# Problemas Encontrados

Durante la implementación se presentaron distintos inconvenientes propios de un despliegue completo.

Entre ellos:

- Problemas de comunicación entre el Dashboard y el Indexer.
- Configuración incorrecta de certificados.
- Variables de entorno relacionadas con Java.
- Reinicio de servicios.
- Configuración de permisos.
- Validación de índices.

Cada uno de estos incidentes fue documentado y resuelto antes de continuar con la implementación del laboratorio.

---

# Solución Aplicada

Los problemas fueron solucionados mediante:

- Revisión de logs.
- Validación de configuración.
- Corrección de certificados.
- Reconfiguración de variables de entorno.
- Reinicio controlado de servicios.
- Verificación mediante comandos administrativos.

---

# Evidencias

Las evidencias consideradas para este laboratorio incluyen:

- Estado de los servicios.
- Capturas del Dashboard.
- Registro del Indexer.
- Estado del Manager.
- Comunicación entre componentes.
- Primer acceso al Dashboard.

Las capturas serán incorporadas conforme avance la documentación del proyecto.

---

# Detecciones Implementadas

En esta etapa únicamente se validó el funcionamiento del SIEM.

Las reglas personalizadas serán desarrolladas en los laboratorios de **Detection Engineering**.

---

# Mapeo MITRE ATT&CK

No aplica.

Este laboratorio corresponde a la implementación de la infraestructura de monitoreo.

---

# Lecciones Aprendidas

- La correcta planificación reduce significativamente los tiempos de implementación.
- La validación de certificados es crítica para la comunicación entre componentes.
- La revisión de logs facilita la resolución de incidentes durante el despliegue.
- Documentar cada cambio permite reproducir el laboratorio de forma consistente.
- Comprender la arquitectura de Wazuh facilita futuras tareas de administración y troubleshooting.

---

# Referencias

- Wazuh Documentation

- OpenSearch Documentation

- Ubuntu Documentation
