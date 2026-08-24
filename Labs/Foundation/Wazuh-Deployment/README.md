# Foundation — Wazuh Deployment

## Objetivo

Implementar una plataforma **SIEM** basada en **Wazuh** que permita centralizar eventos de seguridad, administrar agentes, generar alertas y servir como plataforma principal para actividades de **Security Monitoring**, **Threat Hunting**, **Detection Engineering** e **Incident Response**.

---

## Alcance

Este laboratorio contempla la instalación y configuración inicial de Wazuh sobre un servidor Ubuntu dedicado al laboratorio.

Incluye:

- preparación del servidor;
- instalación de Wazuh Manager;
- instalación y configuración de Wazuh Indexer;
- instalación y configuración de Wazuh Dashboard;
- configuración de Filebeat y certificados;
- validación de servicios;
- acceso a la interfaz web;
- registro inicial de agentes.

La generación y validación detallada de telemetría se documenta en **Telemetry Collection**.

---

## Arquitectura

La plataforma se desplegó en un **Ubuntu Server** con los componentes principales de Wazuh alojados en el mismo servidor del laboratorio. Este patrón corresponde a un despliegue **all-in-one**, aunque internamente los servicios mantienen funciones separadas.

```text
Endpoints
   │
   ▼
Wazuh Agents
   │
   ▼
Wazuh Manager / Analysis Engine
   │
   ▼
Filebeat
   │
   ▼
Wazuh Indexer
   │
   ▼
Wazuh Dashboard
```

### Componentes

| Componente | Función |
|---|---|
| **Wazuh Manager** | Recepción de datos de agentes, análisis de eventos y aplicación del ruleset |
| **Wazuh Indexer** | Almacenamiento, indexación y consulta de datos de seguridad |
| **Wazuh Dashboard** | Visualización, búsqueda y administración mediante interfaz web |
| **Filebeat** | Transporte de alertas y eventos procesados desde el servidor Wazuh hacia el Indexer |
| **Wazuh API** | Interfaz de administración y consulta de funciones del servidor Wazuh |

---

## Tecnologías utilizadas

- Ubuntu Server.
- Wazuh Manager.
- Wazuh Indexer.
- Wazuh Dashboard.
- Filebeat.
- Wazuh API.

---

## Requisitos

Para la implementación se consideró:

- Ubuntu Server actualizado;
- acceso a Internet para instalación y actualización;
- resolución DNS funcional;
- sincronización horaria;
- recursos suficientes de CPU, RAM y almacenamiento;
- conectividad entre endpoints y servidor Wazuh.

---

## Implementación

Las principales actividades realizadas fueron:

1. Preparación del servidor.
2. Actualización del sistema operativo.
3. Descarga de los componentes mediante los procedimientos oficiales de Wazuh.
4. Instalación y configuración de Wazuh Manager.
5. Instalación y configuración de Wazuh Indexer.
6. Instalación y configuración de Wazuh Dashboard.
7. Configuración de certificados.
8. Configuración de Filebeat.
9. Inicio y validación de servicios.
10. Acceso al Dashboard.
11. Registro inicial de agentes.

---

## Configuración

### Wazuh Manager

- gestión de agentes;
- recepción y procesamiento de eventos;
- aplicación de decoders y rulesets;
- generación de alertas.

### Wazuh Indexer

- almacenamiento de información;
- indexación;
- consulta de datos;
- comunicación segura mediante certificados.

### Wazuh Dashboard

- acceso web;
- visualización de alertas y eventos;
- administración y consulta del entorno.

### Filebeat

Configurado para remitir hacia el Indexer los datos procesados por el servidor Wazuh.

---

## Validación

Se verificó el correcto funcionamiento de:

- Wazuh Manager;
- Wazuh Indexer;
- Wazuh Dashboard;
- Filebeat;
- Wazuh API.

Además se comprobó:

- acceso a la interfaz web;
- estado de servicios;
- comunicación entre componentes;
- registro de agentes;
- recepción y visualización de eventos.

---

## Problemas encontrados y troubleshooting

Durante el despliegue se presentaron incidencias propias de la configuración de una plataforma SIEM, entre ellas:

- comunicación entre Dashboard e Indexer;
- certificados;
- permisos;
- variables de entorno y dependencias;
- reinicio y validación de servicios;
- verificación de índices.

La resolución se apoyó en:

- revisión de logs;
- validación de archivos de configuración;
- corrección de certificados y permisos;
- reinicio controlado de servicios;
- comprobaciones administrativas.

---

## Evidencia

Las evidencias consideradas incluyen:

- estado de servicios;
- acceso al Dashboard;
- estado del Manager;
- estado del Indexer;
- comunicación entre componentes;
- registro de agentes;
- eventos y alertas visibles tras las primeras pruebas.

---

## Detecciones implementadas

En esta etapa el objetivo principal fue validar la infraestructura del SIEM. Las detecciones específicas y reglas personalizadas se documentan en **Detection Engineering** y en los proyectos asociados.

---

## Mapeo MITRE ATT&CK

No aplica de forma directa al despliegue de infraestructura. MITRE ATT&CK se utiliza posteriormente para mapear comportamientos, detecciones e investigaciones.

---

## Lecciones aprendidas

- Comprender la separación funcional entre Manager, Indexer y Dashboard facilita el troubleshooting.
- La validación de certificados es crítica para la comunicación entre componentes.
- La revisión de logs es fundamental durante el despliegue.
- Documentar cada cambio mejora la repetibilidad del laboratorio.
- Un despliegue all-in-one puede mantener los componentes lógicamente separados aunque residan en el mismo servidor.

---

## Referencias

- Wazuh Documentation.
- OpenSearch Documentation.
- Ubuntu Documentation.
