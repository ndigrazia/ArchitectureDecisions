# ADR CTR 0006. Recepción de eventos del sistema operativo en el proceso que ejecuta en el contenedor

## Keywords

containerizing, container, imagen, uso, contenedor, producción, recepción, eventos, sistema operativo, orquestadores.

## Status

Accepted

## Context

La fase siguiente a la construcción de la imagen de contenedor es registrarla en un servidor de registro (container image registry) el cual, servirá de punto de partida para la ejecución de la imagen dentro de un motor de orquestación (Docker Swarm, Kubernetes, etc.). 

Toda imagen de contenedor contiene un proceso (o aplicación) que es el encargado de brindar los servicios del contenedor.

El motor de orquestación envía señales para gobernar el contenedor durante su ejecución. La manera en la cual iniciamos el proceso (o la aplicación) del contenedor al momento de su ejecución, tiene impacto directo en el procesamiento de las señales enviadas desde el motor de orquestación al contenedor en ejecución. Es decir, si el proceso del contenedor se inicia indirectamente no se garantiza que el mismo recibirá estas señales y de ser así, señales como por ejemplo: SIGTERM o SIGKILL no serán procesadas, impidiendo que los servicios del contenedor finalicen limpiamente.

## Decision

Aseguramos que todas las señales enviadas desde el motor de orquestación sean recibidas por el proceso (o aplicación) que corre en el contenedor.

Actualmente, tenemos dos alternativas para poder lograr este requerimiento:

1. Iniciar el shell del sistema operativo y luego ejecutar el proceso del contenedor. En este caso, es posible que el shell no envíe las señales al proceso del contenedor.
   
2. Iniciar directamente el proceso sin usar el shell del sistema operativo. En este caso, el proceso actuará como proceso principal (PID 1) tomando las responsabilidades de inicio del sistema operativo y de sus procesos. Estas funcionalidades especiales hacen que el proceso del contenedor tenga más responsabilidad de la requerida y además, las mayorías de los runtimes (java, node.js, etc) sobre los cuales corre el proceso del contenedor no soportan actuar como proceso principal, ocasionando un comportamiento inesperado en los servicios del contenedor.

Como vemos, necesitamos disponer de una herramienta que actué como proceso de inicio y además, envíe las señales al proceso del contenedor.

## Consequences

Requerimos seleccionar una herramienta que actué como un proceso de inicio (por ejemplo dumb-init), que envíe las señales al proceso del contenedor y que, tenga una huella reducida para no agregar mayor tamaño a la imagen del contenedor ni incrementar sus vulnerabilidades.

Requerimos iniciar el proceso del contenedor a través de la herramienta seleccionada como  proceso de inicio (PID 1). Para ello, en el archivo que describe los pasos de construcción de la imagen del contenedor (por ejemplo, Dockerfile), requerimos usar la directiva de inicio del proceso con la herramienta seleccionada (por ejemplo, CMD [<herramienta>, <runtime>, <aplicación>]).

El siguiente es un ejemplo de un servicio construido usando Docker que cumple con lo solicitado:

```
FROM node:16.17.0-bullseye-slim
RUN apt-get update && apt-get install -y --no-install-recommends dumb-init
...
# Herramienta que actúa como proceso de inicio
CMD ["dumb-init", "node", "server.js"]
```

