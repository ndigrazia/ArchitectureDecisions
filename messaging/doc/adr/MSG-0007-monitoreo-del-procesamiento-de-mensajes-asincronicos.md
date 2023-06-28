# ADR MSG 0007. Monitoreo del procesamiento de mensajes asincronicos

## Keywords

messaging, message, asincrónica, mensaje, cola, soporte, monitoreo, observabilidad.

## Status

Accepted

## Context

Observar la utilización de la cola es fundamental para comprender la carga de trabajo y el estado del sistema. 

Las métricas como la cantidad de mensajes pendientes, la cantidad de consumidores y la tasa de consumo permiten que el sistema pueda diagnosticarse y repararse, ajustando la cantidad de consumidores o estrangulando al productor.

## Decision

Monitoreamos el procesamiento de mensajes asincrónicos en colas de mensajerías y, actuamos en consecuencia.

Las estrategias de monitoreo y los mecanismos para responder a las situaciones que se presenten durante el funcionamiento del sistema varían según los requerimientos o definiciones del negocio.

## Consequences

Requerimos establecer la lógica o la estrategia de monitoreo del consumo de los mensajes en la cola de mensajería y, definir la lógica para reaccionar y adecuar el procesamiento de los mensajes a las necesidades del negocio. 

Si durante el análisis se determina que el rendimiento de los consumidores no es suficiente, incrementar el número de los mismos o viceversa. 

En el caso de no ser posible el uso de más consumidores (debido al costo que esto supone), ralentizar los productores via una señal hasta que el consumidor pueda ponerse al día (back pressure).
