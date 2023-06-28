# ADR MS 0008. Trazabilidad distribuida

## Keywords

microservicio, trazabilidad, despliegue, soporte.

## Status

Accepted

## Context

Conocer el camino que sigue una petición desde su inicio hasta su final puede ayudar en la resolución de problemas. El rastreo distribuido muestra la ruta que sigue una solicitud a medida que viaja a través de un sistema distribuido. A medida que las solicitudes viajan entre los servicios, cada segmento se registra. Todos los tramos de una solicitud se combinan en un solo rastreo distribuido para dar una imagen de una solicitud completa. Una vez capturados los rastros de una petición, se puede proceder a analizarlos y resolver inconvenientes de una forma más fácil y rápida.

## Decision

Exponemos y usamos mecanismos para rastrear el flujo de un pedido a través del sistema distribuido con el objetivo de diagnosticar problemas o detectar anomalías.

## Consequences

Requerimos el uso de alguna de las siguientes estrategias:

- Uso de un service mesh (malla de servicios) para recopilar la traza de los pedidos, mediante la propagación del contexto de traza (Trace Context Propagation).

- Publicación de la traza mediante el uso de librerías o bibliotecas externas.

En ambos casos se necesita un sistema de monitoreo donde se puedan analizar las trazas informadas.

Se prefiere el empleo de una malla de servicio dado que es menos invasiva a la solución de librerías o de frameworks.
