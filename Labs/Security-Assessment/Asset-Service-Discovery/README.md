# Asset & Service Discovery — Controlled Security Assessment

## Objetivo

Documentar actividades prácticas de **descubrimiento de activos y servicios** realizadas en un entorno controlado y autorizado, como base para evaluaciones de superficie de ataque y gestión de vulnerabilidades.

## Trabajo realizado

Las actividades incluyeron:

- definición previa de alcance y targets autorizados;
- validación de direcciones IP y redes CIDR;
- descubrimiento de hosts activos;
- identificación de puertos y servicios expuestos;
- ejecución controlada de Nmap desde Linux/Kali;
- separación entre fase de discovery y enumeración de servicios;
- generación de resultados estructurados para análisis posterior;
- conservación de evidencia técnica y verificación de resultados.

## Metodología de trabajo

El proceso se realizó siguiendo **documentación técnica de las herramientas, procedimientos de laboratorio y validaciones de seguridad definidas antes de la ejecución**. Se utilizó **inteligencia artificial como guía asistida** para estructurar procedimientos, revisar parámetros, apoyar troubleshooting y transformar resultados técnicos en documentación clara.

Toda ejecución fue validada directamente en el entorno. La IA no sustituyó la comprobación de alcance, la autorización ni la verificación de los resultados obtenidos.

## Flujo de trabajo

```text
Scope autorizado
      ↓
Validación IP/CIDR
      ↓
Host Discovery
      ↓
Service Discovery
      ↓
Resultado estructurado
      ↓
Validación / evidencia
      ↓
Security Assessment
```

## Principios aplicados

- alcance explícito;
- ejecución no destructiva;
- parámetros controlados;
- separación entre descubrimiento y análisis;
- trazabilidad de resultados;
- preservación de evidencia;
- mínima exposición de información sensible.

## Capacidades demostradas

- Asset Discovery.
- Service Discovery.
- Attack Surface Assessment.
- Nmap.
- Kali Linux.
- IP/CIDR validation.
- Scope control.
- Evidence handling.
- Structured technical outputs.

## Resultado

Se validó un flujo reproducible para identificar activos y servicios dentro de un alcance autorizado, generando información técnica utilizable como entrada para actividades posteriores de evaluación de vulnerabilidades y análisis defensivo.