# Foundation - Environment Setup

## Objetivo

Diseñar e implementar la infraestructura base del laboratorio de ciberseguridad que servirá como plataforma para desarrollar actividades de **Security Monitoring**, **Threat Hunting**, **Detection Engineering** e **Incident Response**.

El objetivo principal es disponer de un entorno controlado donde sea posible generar telemetría, simular escenarios de ataque, validar reglas de detección e investigar incidentes de seguridad.

---

# Alcance

Este laboratorio contempla la construcción de la infraestructura inicial necesaria para el funcionamiento del entorno de prácticas.

Incluye:

- Diseño de la arquitectura del laboratorio.
- Instalación del hipervisor.
- Creación de máquinas virtuales.
- Configuración de red.
- Comunicación entre equipos.
- Validación de conectividad.

Este laboratorio no contempla la instalación de Wazuh, la cual será documentada en el laboratorio **Wazuh Deployment**.

---

# Arquitectura

El laboratorio fue implementado utilizando **VirtualBox** como plataforma de virtualización.

La infraestructura inicial está compuesta por los siguientes equipos:

| Equipo | Sistema Operativo | Función |
|---------|-------------------|----------|
| Wazuh Server | Ubuntu Server | SIEM |
| Windows 11 | Windows 11 Pro | Endpoint Windows |
| Ubuntu | Ubuntu Desktop | Endpoint Linux |
| Kali Linux | Kali Linux | Simulación de ataques |

---

# Topología de Red

Se implementaron dos adaptadores de red por máquina virtual.

## Adaptador 1

- Tipo: NAT
- Función: Acceso a Internet
- Configuración: DHCP

Permite:

- Descargar actualizaciones.
- Instalar paquetes.
- Acceder a repositorios oficiales.

---

## Adaptador 2

- Tipo: Host-Only
- Función: Red interna del laboratorio.

Características:

- Comunicación entre máquinas virtuales.
- Aislamiento del laboratorio respecto a la red corporativa.
- Generación de tráfico controlado.

---

# Tecnologías Utilizadas

## Virtualización

- VirtualBox

## Sistemas Operativos

- Ubuntu Server
- Ubuntu Desktop
- Windows 11 Pro
- Kali Linux

## Administración

- SSH
- PowerShell
- Bash

---

# Requisitos

Para la implementación del laboratorio se consideraron los siguientes recursos mínimos:

- Procesador con virtualización habilitada.
- Memoria RAM suficiente para ejecutar múltiples máquinas virtuales.
- Espacio de almacenamiento disponible para snapshots y laboratorios.
- Conectividad a Internet para descarga de paquetes.

---

# Implementación

Durante la construcción del laboratorio se realizaron las siguientes actividades:

1. Instalación de VirtualBox.
2. Creación de las máquinas virtuales.
3. Configuración de CPU y memoria.
4. Configuración de almacenamiento.
5. Configuración de adaptadores de red.
6. Instalación de los sistemas operativos.
7. Configuración inicial de usuarios.
8. Actualización del sistema operativo.
9. Validación de conectividad entre equipos.

---

# Configuración

Cada máquina virtual fue configurada de acuerdo con su función dentro del laboratorio.

Las configuraciones incluyen:

- Nombre del equipo.
- Dirección IP.
- Adaptadores de red.
- Usuarios administrativos.
- Acceso remoto.
- Sincronización de hora.

La configuración específica de cada servidor será documentada en los laboratorios correspondientes.

---

# Validación

Se realizaron pruebas para verificar:

- Comunicación entre máquinas virtuales.
- Acceso a Internet.
- Resolución DNS.
- Acceso mediante SSH.
- Estabilidad del laboratorio.

Todas las pruebas fueron satisfactorias antes de continuar con la instalación del SIEM.

---

# Evidencias

Durante este laboratorio se documentan las siguientes evidencias:

- Arquitectura del laboratorio.
- Configuración de VirtualBox.
- Configuración de red.
- Capturas de las máquinas virtuales.
- Validación de conectividad.
- Estado inicial de cada sistema operativo.

Las evidencias gráficas serán incorporadas conforme avance la documentación del proyecto.

---

# Detecciones Implementadas

No aplica.

Este laboratorio corresponde únicamente a la preparación de la infraestructura.

Las primeras detecciones serán implementadas durante los laboratorios de **Security Monitoring**.

---

# Mapeo MITRE ATT&CK

No aplica.

Este laboratorio corresponde a la fase de construcción del entorno de trabajo.

---

# Lecciones Aprendidas

- La planificación de la arquitectura simplifica la administración del laboratorio.
- La separación de redes permite generar escenarios de prueba de forma segura.
- Documentar la infraestructura desde el inicio facilita el crecimiento del laboratorio.
- Una correcta organización mejora la repetibilidad de los laboratorios futuros.

---

# Referencias

- VirtualBox Documentation
- Ubuntu Documentation
- Microsoft Learn
- Wazuh Documentation
