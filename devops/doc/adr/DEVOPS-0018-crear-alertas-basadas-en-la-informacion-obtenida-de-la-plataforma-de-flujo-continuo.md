# ADR DEVOPS 0018. Crear alertas basadas en la información obtenida de la plataforma de flujo continuo

Date: 2023-01-20

## Keywords

devops, alerta, alarma, notificación, infraestructura, continuo, entrega, despliegue, flujo, proceso, evento.

## Status

Accepted

## Context

La información almacenada en las soluciones de registro y de monitoreo no solo ayuda a resolver inconvenientes en forma temprana, sino que también, puede ser empleada para configurar alertas con el objetivo de conocer los problemas en tiempo real y así, permitir actuar rápidamente, manteniendo a los miembros de los equipos seguros ante situaciones críticas.

Recibir notificaciones de eventos como consecuencias de fallas significativamente más altas de lo habitual es uno de los casos de uso más comunes en los equipos de DevOps.

## Decision

Definiremos alertas basadas en la información obtenida de la plataforma de flujo continuo para permitir a los miembros de los equipos conocer los problemas que suceden en la solución de flujo continuo en el mismo momento que ocurren.

## Consequences

Disponer de un mecanismo de alertas ayuda a brindar un mejor servicio, a prevenir crisis, a disponer de información precisa durante una emergencia, a alertar a un gran número de personas lo más rápido posible, a informar al instante de lo que está sucediendo, entre otras cosas. Sin embargo, se debe considerar los siguientes desafíos:

- Habilidades requeridas en los administradores para configurar y aprovisionar la infraestructura de notificación.

- Definición y configuración de reglas de notificación teniendo en cuenta la importancia del impacto de la incidencia en el negocio.
