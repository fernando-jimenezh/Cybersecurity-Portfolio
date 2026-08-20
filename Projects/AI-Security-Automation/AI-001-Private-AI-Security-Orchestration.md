# AI-001 — Private AI Security Orchestration Lab

## Resumen ejecutivo

Este proyecto documenta el diseño e implementación inicial de una arquitectura privada de IA orientada a **automatización técnica y operaciones de seguridad** dentro de un laboratorio controlado.

El objetivo fue integrar un **LLM local** con una capa de agente/API capaz de interpretar solicitudes en lenguaje natural y transformarlas en acciones técnicas autorizadas, manteniendo una separación estricta entre **razonamiento** y **ejecución**.

La implementación fue diseñada bajo un principio central:

> El modelo puede interpretar y solicitar acciones, pero no dispone de acceso irrestricto al sistema operativo ni ejecuta comandos arbitrarios directamente.

La documentación pública ha sido sanitizada para demostrar las capacidades técnicas sin revelar información operativa sensible del entorno donde se desarrolló la práctica.

---

## Objetivo

Diseñar y validar un flujo donde una solicitud en lenguaje natural pueda:

1. ser interpretada por un modelo de IA local;
2. convertirse en una intención técnica;
3. pasar por controles de autorización y validación;
4. ejecutar una herramienta previamente permitida;
5. obtener un resultado real desde un runner Linux;
6. procesar la salida mediante un parser determinístico;
7. devolver un resultado estructurado para su posterior interpretación por IA.

---

## Alcance

El proyecto cubre:

- despliegue de un LLM local;
- interfaz Web para interacción;
- integración mediante API;
- diseño de un agente de orquestación;
- separación entre reasoning y execution;
- control de herramientas autorizadas;
- validación de parámetros;
- ejecución técnica sobre Linux;
- timeouts y auditoría;
- parsing determinístico;
- respuesta estructurada;
- validación end-to-end de una operación técnica real.

No forma parte del alcance público documentar credenciales, direccionamiento interno, topología real, endpoints privados, nombres de sistemas internos ni configuraciones sensibles.

---

## Arquitectura lógica

```text
Usuario
  │
  ▼
Web Interface
  │
  ▼
Local LLM
  │
  ▼
AI Agent / API
  │
  ▼
Authorization & Validation
  │
  ▼
Controlled Linux Runner
  │
  ▼
Approved Security / Infrastructure Tool
  │
  ▼
Deterministic Parser
  │
  ▼
Structured Result
  │
  ▼
AI-assisted Interpretation
```

La arquitectura evita el patrón:

```text
LLM → unrestricted shell
```

Y utiliza en su lugar:

```text
LLM
 ↓
intent
 ↓
approved tool
 ↓
validated parameters
 ↓
controlled execution
 ↓
structured evidence
```

---

## Componentes técnicos

### Local LLM Runtime

Se desplegó un runtime local para ejecutar modelos LLM sin depender de una API externa para las operaciones básicas del laboratorio.

Tecnología utilizada:

- **Ollama**.

El runtime permite cargar y consumir modelos mediante una API local, manteniendo el procesamiento dentro de la infraestructura del laboratorio.

### Web Interface

Se integró una interfaz Web para facilitar la interacción con el modelo y validar el flujo conversacional.

Tecnología utilizada:

- **Open WebUI**.

La interfaz se mantiene separada del motor de inferencia y de la capa de ejecución técnica.

### Agent / API Layer

Se implementó una capa intermedia responsable de:

- interpretar solicitudes;
- identificar la tool solicitada;
- validar argumentos;
- comprobar que la operación esté permitida;
- controlar el flujo de ejecución;
- registrar resultados;
- entregar datos estructurados al modelo.

Esta separación evita que el LLM tenga control directo sobre el runner.

### Controlled Linux Runner

La ejecución real se realiza en un sistema Linux separado de la capa de IA.

El runner tiene la responsabilidad de ejecutar únicamente herramientas previamente autorizadas dentro del alcance del laboratorio.

Este diseño permite separar:

```text
Reasoning Plane
      │
      ▼
Control Plane
      │
      ▼
Execution Plane
```

### Deterministic Parser

La salida de las herramientas no se entrega directamente al LLM como única fuente de verdad.

Primero se procesa mediante parsers determinísticos para obtener campos estructurados como:

- estado de ejecución;
- resultado principal;
- métricas relevantes;
- errores;
- timestamps;
- información normalizada.

Esto reduce el riesgo de que el modelo interprete incorrectamente una salida técnica ambigua.

---

## Controles de seguridad aplicados

### Tool Allowlist

Solo pueden ejecutarse funciones previamente definidas.

El modelo no puede crear libremente nuevos comandos del sistema operativo.

### Parameter Validation

Los parámetros son validados antes de ser enviados al runner.

El objetivo es impedir que una entrada conversacional se transforme directamente en una instrucción de shell arbitraria.

### Scope Control

Las operaciones deben permanecer dentro del alcance definido para el laboratorio.

### Timeouts

Las ejecuciones técnicas utilizan límites temporales para evitar procesos bloqueados o consumo indefinido de recursos.

### Auditing

El flujo está diseñado para registrar al menos:

- acción solicitada;
- tool utilizada;
- resultado;
- estado de ejecución;
- momento de la operación.

### Separation of Duties

La IA no controla directamente el sistema operativo.

```text
LLM       → interpreta
Agent/API → autoriza y coordina
Runner    → ejecuta
Parser    → valida y estructura
LLM       → explica
```

---

## Validación end-to-end

Como prueba inicial se utilizó una operación simple de verificación de conectividad dentro del laboratorio.

El flujo validado fue:

```text
Solicitud en lenguaje natural
        ↓
Interpretación de intención
        ↓
Tool permitida
        ↓
Validación de parámetros
        ↓
Ejecución real en Linux
        ↓
Resultado de conectividad
        ↓
Parser determinístico
        ↓
Resultado estructurado
        ↓
Interpretación asistida por IA
```

La prueba confirmó que la arquitectura podía completar el ciclo desde la solicitud hasta la ejecución real sin otorgar al modelo un shell arbitrario.

No se publican el activo utilizado, direccionamiento, hostname ni otros identificadores del entorno.

---

## Capacidades demostradas

Este proyecto demuestra experiencia práctica en:

- Local AI deployment.
- LLM runtime administration.
- AI integration.
- REST APIs.
- Agent architecture.
- Security automation.
- Tool orchestration.
- Linux administration.
- Input validation.
- Allowlisting.
- Auditability.
- Deterministic parsing.
- Structured evidence handling.
- Secure-by-design automation.
- AI-assisted technical workflows.

---

## Aplicación a Security Operations

La misma arquitectura puede evolucionar para soportar, bajo autorización y dentro de un alcance controlado:

- asset availability checks;
- infrastructure discovery;
- service identification;
- TLS checks;
- log analysis;
- vulnerability assessment support;
- evidence summarization;
- detection analysis;
- technical report drafting;
- control validation;
- security knowledge retrieval.

Cada nueva capacidad debe implementarse como una tool explícita, con validación, timeout, auditoría y parser propios.

---

## Consideraciones de privacidad

Este proyecto fue diseñado considerando que los entornos de ciberseguridad pueden contener información sensible.

Por esa razón, la documentación pública no expone:

- organizaciones involucradas;
- datos de clientes;
- nombres internos de activos;
- IPs privadas;
- segmentos de red;
- credenciales;
- claves API;
- tokens;
- rutas internas;
- hashes operativos;
- endpoints administrativos;
- reglas propietarias;
- documentación empresarial privada.

La información publicada es suficiente para demostrar el conocimiento técnico sin comprometer la seguridad del entorno real.

---

## Limitaciones actuales

La implementación corresponde a una etapa inicial y controlada del laboratorio.

El modelo local utilizado es adecuado para validar integración y tool orchestration, pero no se asume que pueda reemplazar modelos de mayor capacidad para razonamiento complejo.

La cantidad de tools autorizadas se mantiene deliberadamente reducida mientras se valida la arquitectura de seguridad.

---

## Próximos pasos

La evolución prevista del laboratorio incluye, cuando exista evidencia real para documentarlo:

- incorporación gradual de nuevas tools autorizadas;
- RAG sobre documentación técnica sanitizada;
- análisis asistido de logs;
- integración con workflows de Vulnerability Management;
- correlación de evidencia;
- report generation basada exclusivamente en resultados confirmados;
- model routing local/híbrido según sensibilidad y complejidad;
- controles adicionales de autorización y gobierno de IA.

---

## Conclusión

El laboratorio permitió validar una arquitectura de **IA privada aplicada a operaciones técnicas de seguridad** basada en separación de funciones, ejecución controlada y evidencia estructurada.

La principal conclusión es que un LLM puede utilizarse como capa de interpretación y orquestación sin convertirlo en un operador con acceso irrestricto al sistema.

El diseño combina conocimientos de **ciberseguridad, Linux, APIs, automatización, arquitectura de agentes e integración de IA**, proporcionando una base escalable para futuros casos de AI-assisted Security Operations.
