# ADR CTR 0007. Finalización limpia de contenedores en ejecución

Date: 2023-09-07

## Keywords

containerizing, container, imagen, uso, contenedor, producción, finalización, limpia, eventos, recepción, sistema operativo, orquestadores, cierre.

## Status

Accepted

## Context

Cuando el proceso (o la aplicación) que corre en el contenedor es capaz de recibir las señales enviadas desde el motor de orquestación puede actuar en consecuencia. En tal caso, si una señal de interrupción (SIGINT) es recibida, puede provocar la finalización abrupta del proceso, causando que los usuarios conectados al mismo sean desconectados inmediatamente, afectando su experiencia. 

Con el fin de proveer una mejor de experiencia a los usuarios, debemos ser capaces de poder administrar las señales de interrupción que llegan al proceso del contenedor. 

## Decision

Configuramos un controlador de eventos (event handler) para las señales de terminación del contenedor.

El controlador de eventos debe ser capaz de realizar operaciones de cierres elegantes o limpias como respuesta a las señales de terminación.

Las operaciones de cierres elegantes implican realizar acciones como el cierre de conexiones de las bases de datos, cierre de conexiones de red, etc.  

## Consequences

Requerimos establecer un controlador de eventos para las distintas señales de terminación (SIGINT, SIGTERM, etc.).

Requerimos que el controlador realice cierres limpios de sus recursos o servicios.

Requerimos que el controlador finalice el proceso que corre en el contenedor. 

El siguiente es un ejemplo de un servicio implementado en el Framework Node.js que cumple con lo solicitado:

```
async function closeGracefully(signal) {
   await fastify.close()
  process.kill(process.pid, signal);
}

//Controlador de eventos para las distintas señales de terminación
process.once('SIGINT', closeGracefully)
process.once('SIGTERM', closeGracefully)
```

