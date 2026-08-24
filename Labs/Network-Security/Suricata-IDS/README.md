# Suricata IDS — Network Security Monitoring

## Objetivo

Documentar la implementación práctica de **Suricata** como sensor IDS dentro de un laboratorio controlado de ciberseguridad, orientado a **Network Security Monitoring**, generación de alertas y futura correlación con el SIEM.

## Trabajo realizado

La implementación contempló:

- instalación de Suricata en Linux;
- identificación y selección de la interfaz de red de monitoreo;
- configuración del alcance de red (`HOME_NET`);
- habilitación y actualización de reglas;
- validación del servicio;
- revisión de logs y eventos;
- generación de telemetría estructurada mediante `eve.json`;
- comprobación de alertas en un entorno autorizado.

## Metodología de trabajo

El despliegue se realizó combinando **documentación técnica oficial, manuales de referencia y validación práctica en laboratorio**. Se utilizó **inteligencia artificial como apoyo técnico** para organizar pasos, interpretar errores, contrastar configuraciones y documentar resultados.

La IA se utilizó como herramienta de asistencia; las configuraciones, comandos, estados de servicio y resultados fueron verificados directamente sobre el entorno.

## Flujo de monitoreo

```text
Tráfico de red
      ↓
Suricata IDS
      ↓
Rules Engine
      ↓
eve.json / alerts
      ↓
Network Security Monitoring
      ↓
SIEM / análisis defensivo
```

## Capacidades demostradas

- Network IDS.
- Network Security Monitoring.
- Linux administration aplicada a seguridad.
- Configuración de reglas IDS.
- Análisis de logs de red.
- Generación de telemetría de seguridad.
- Troubleshooting basado en logs.
- Integración conceptual IDS → SIEM.

## Evidencia

La validación se basó en estados de servicio, logs generados por Suricata, archivos de eventos y alertas observadas durante pruebas controladas.

No se publican direcciones de red privadas, identificadores internos ni configuraciones sensibles.

## Relación con otros laboratorios

Este laboratorio complementa:

- Wazuh SIEM Deployment.
- Telemetry Collection.
- Security Monitoring.
- Detection Engineering.
- Threat Hunting.

## Resultado

Se obtuvo un sensor IDS operativo capaz de inspeccionar tráfico, aplicar reglas de detección y producir eventos utilizables para monitoreo e investigación defensiva.