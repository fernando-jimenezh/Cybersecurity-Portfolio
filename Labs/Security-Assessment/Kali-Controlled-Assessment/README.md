# Kali Linux — Controlled Security Assessment Environment

## Objetivo

Documentar el uso de **Kali Linux** como entorno técnico controlado para actividades de evaluación de seguridad, discovery, enumeración, validación y pruebas autorizadas dentro del laboratorio.

## Trabajo realizado

El entorno se preparó para:

- ejecutar herramientas de evaluación de seguridad desde Linux;
- trabajar sobre redes de laboratorio aisladas;
- realizar host y service discovery;
- validar conectividad y alcance antes de ejecutar pruebas;
- centralizar herramientas de assessment;
- separar el entorno de evaluación de los sistemas objetivo;
- generar resultados técnicos para análisis posterior.

## Metodología de trabajo

La preparación y operación se apoyó en **documentación técnica de Kali Linux y de las herramientas utilizadas**, procedimientos propios de laboratorio y **asistencia de inteligencia artificial** para estructurar pasos, revisar configuraciones, apoyar troubleshooting y documentar resultados.

Las acciones ejecutadas fueron verificadas directamente en el entorno y restringidas a sistemas autorizados. La IA no reemplazó la definición de alcance ni la validación técnica.

## Arquitectura conceptual

```text
Kali Linux
   │
   ├── Discovery
   ├── Enumeration
   ├── Validation
   └── Security Tools
          │
          ▼
   Red de laboratorio
          │
          ▼
   Targets autorizados
```

## Controles aplicados

- targets definidos;
- validación previa de IP/CIDR;
- preferencia por pruebas read-only y no destructivas;
- separación de redes y entornos;
- registro de resultados;
- revisión antes de ampliar alcance.

## Capacidades demostradas

- Kali Linux.
- Security Assessment Environment.
- Linux networking.
- Nmap y herramientas de discovery.
- Scope control.
- Controlled execution.
- Security validation.
- Troubleshooting técnico.

## Resultado

Se dispuso de un entorno reproducible y aislado para realizar actividades de evaluación de seguridad de forma controlada, sirviendo como plataforma base para los laboratorios de Asset & Service Discovery y Vulnerability Assessment.