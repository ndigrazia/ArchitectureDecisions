# ADR DEVOPS 0016. Monitoreo de telemetría de la plataforma de flujo continuo

Date: 2023-01-19

## Keywords

devops, monitoreo, automático, infraestructura, continuo, métrica, entrega, despliegue, flujo, proceso.

## Status

Accepted

## Context

¿Cómo sabe si la infraestructura que soporta la solución de flujo continuo está funcionando correctamente?

El monitoreo de la infraestructura y de la aplicación de la solución de flujo continuo ayuda a identificar problemas en forma temprana, permitiendo minimizar el tiempo de inactividad de la solución y así, evitar la interrupción de los procesos automáticos y continuos usados en el desarrollo y el mantenimiento de las aplicaciones en la nube.

## Decision

Usaremos una solución de monitoreo para observar la telemetría de la plataforma de flujo continuo.

La solución de monitoreo se puede dividir en tres partes:

- Metrics collector: un agente recopilador de métricas que recoge las métricas de la solución y las envía a un repositorio de datos.
  
- Metrics repository: Base de datos de series temporales optimizada para almacenamiento de alta disponibilidad que recibe la telemetría procedente de los recopiladores de métricas.

- Observability platform: Plataforma de visualización y de consulta de datos de telemetría almacenados en el repositorio de datos.
  
## Consequences

El uso de soluciones de monitoreo de telemetría permite realizar un seguimiento de las métricas de la plataforma, garantizando la disponibilidad de sus servicios y la entrega continua de valor al negocio. Sin embargo, para alcanzar este beneficio, se debe considerar los siguientes desafíos:

- La elección del software usado como solución de monitoreo de telemetría.
  
- Habilidades requeridas en los administradores para configurar y aprovisionar la infraestructura de la solución de monitoreo.
  
- Definición y configuración de las métricas que impactan en el negocio y como consecuencia, serán observadas.

- Creación de pizarras (dashboard) basadas en las métricas consideradas.
