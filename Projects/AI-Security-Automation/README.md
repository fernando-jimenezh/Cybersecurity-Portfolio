# AI Security Automation

Esta sección documenta proyectos de **IA aplicada a operaciones de seguridad y automatización técnica** desarrollados en un laboratorio propio y controlado.

El objetivo no es presentar experiencia como AI Engineer, sino demostrar capacidad práctica para **desplegar, integrar y gobernar modelos de IA dentro de arquitecturas técnicas de ciberseguridad**.

<p align="center">
  <a href="../README.md"><strong>← Projects</strong></a> ·
  <a href="../../README.md"><strong>Portafolio</strong></a>
</p>

---

## Principios

Los proyectos de esta categoría siguen cinco principios:

1. **El LLM interpreta; no obtiene shell irrestricto.**
2. **Las acciones técnicas deben pasar por una capa de control.**
3. **Los parámetros y el alcance deben validarse antes de ejecutar.**
4. **Los resultados técnicos deben estructurarse antes de ser interpretados por IA.**
5. **La documentación pública debe demostrar capacidad sin revelar información operativa sensible.**

## Arquitectura conceptual

```text
Usuario
  ↓
Interfaz Web
  ↓
LLM local
  ↓
Agente / API
  ↓
Policy & Validation
  ↓
Runner Linux
  ↓
Tool autorizada
  ↓
Parser determinístico
  ↓
Resultado estructurado
  ↓
Análisis asistido por IA
```

## Proyectos

| ID | Proyecto | Estado |
|---|---|---|
| **AI-001** | [Private AI Security Orchestration Lab](AI-001-Private-AI-Security-Orchestration.md) | Implementación inicial validada |

## Capacidades técnicas demostradas

- Local LLM deployment.
- Ollama runtime.
- Open WebUI.
- REST API integration.
- Agent architecture.
- Tool orchestration.
- Linux-based execution runner.
- Parameter validation.
- Tool allowlisting.
- Timeouts y auditing.
- Deterministic parsing.
- Structured technical outputs.
- AI-assisted interpretation.
- Separation of duties entre reasoning y execution.

## Protección de información

La documentación de esta sección está deliberadamente sanitizada. No se publican:

- nombres de organizaciones o sistemas internos;
- direcciones IP o topologías privadas;
- hostnames internos;
- credenciales, tokens o secretos;
- endpoints administrativos;
- rutas internas sensibles;
- hashes de artefactos operativos;
- información de clientes;
- reglas empresariales propietarias;
- configuraciones que permitan reproducir accesos internos.

Solo se exponen los elementos necesarios para demostrar la arquitectura, metodología y conocimientos técnicos adquiridos.
