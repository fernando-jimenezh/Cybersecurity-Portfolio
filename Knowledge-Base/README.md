# Knowledge Base

Esta sección reúne únicamente documentación técnica relacionada con tecnologías, metodologías y conceptos utilizados de forma práctica dentro del laboratorio y de las investigaciones publicadas en este portafolio.

> La Knowledge Base no pretende ser una enciclopedia general de ciberseguridad. Su función es documentar fundamentos que tengan relación directa con evidencia, casos o implementaciones realizadas.

<p align="center">
  <a href="../README.md"><strong>← Portafolio</strong></a> ·
  <a href="../Projects/README.md"><strong>Investigaciones</strong></a> ·
  <a href="../Labs/Foundation/Environment-Setup/README.md"><strong>Laboratorio</strong></a>
</p>

---

## Áreas de conocimiento aplicadas

### SIEM & Security Monitoring

- Arquitectura y operación de SIEM.
- Ingesta y correlación de eventos.
- Wazuh Manager, Indexer, Dashboard y Agents.
- Rulesets, alertas y validación de detecciones.

### Windows Security

- Windows Event Logs.
- Sysmon.
- Process Creation.
- PowerShell Logging.
- Parent-child process relationships.
- Análisis de línea de comandos.

### Linux Security

- Syslog.
- auditd.
- journalctl.
- Procesos, permisos y registros.

### Detection Engineering

- Validación de reglas.
- Lógica de detección.
- Sigma.
- Cobertura y mapeo MITRE ATT&CK.
- Revisión de contenido nativo antes de crear reglas personalizadas.

### Threat Hunting

- Hunting basado en hipótesis.
- Behavioral Analysis.
- Correlación de endpoint, usuario, procesos y comandos.
- Hunting basado en MITRE ATT&CK.

### Networking & Infrastructure Security

- TCP/IP, DNS, DHCP, HTTP/HTTPS, SSH, RDP, SMB, LDAP y Kerberos.
- Redes de laboratorio y virtualización.
- Observabilidad y análisis de conectividad.

## Criterio de publicación

Un documento nuevo debe cumplir al menos una de estas condiciones:

1. Explicar una tecnología utilizada en un caso publicado.
2. Documentar una metodología aplicada en una investigación.
3. Registrar un procedimiento técnico validado en laboratorio.
4. Servir como referencia para reproducir o comprender evidencia existente.

La prioridad seguirá siendo mantener una base pequeña, útil y verificable antes que publicar grandes volúmenes de teoría sin aplicación práctica.

## Próxima evolución

A medida que el portafolio crezca, esta sección podrá incorporar documentos independientes sobre temas como:

```text
Knowledge-Base/
├── Wazuh/
├── Windows/
├── Linux/
├── MITRE-ATTACK/
├── Detection-Engineering/
├── Threat-Hunting/
└── Networking/
```

Las carpetas se crearán únicamente cuando exista contenido técnico suficiente para justificarlas.
