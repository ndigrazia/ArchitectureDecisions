# ADR MS 0004. Despliegue mediante pipeline

Date: 2022-08-17

## Keywords

microservicio, pipeline, despliegue, contenedor, fuente.

## Status

Accepted

Referenced by [ADR MS 0003. Empaquetado del micro servicio como imagen de contenedor](MS-0003-empaquetado-del-microservicio-como-imagen-de-contenedor.md)

## Context

La entrega continua es un proceso ágil en el que el software se construye continuamente con la ayuda de un pipeline o tubería. 

Dado que los microservicios representan aplicaciones que se pueden implementar de forma independiente, pueden hacer uso de este mecanismo para su construcción, eliminado las tareas manuales del proceso de desarrollo de software que ocasionan demora en la entrega del artefacto a producción o, posibilitan altos índices de errores.

## Decision

Desplegamos el microservicio usando un pipeline de despliegue.

Al contar con un pipeline automatizado de despliegue se facilita la implementación de la construcción, testeo y despliegue de la aplicación, permitiendo una rápida retro-alimentación de los problemas, disponer de un mismo proceso en distintos entornos, reducir los tiempos de ejecución de las tareas, las cuales se pueden ejecutar varias veces diariamente, favoreciendo la confianza en el proceso.

## Consequences

Requerimos el uso de un entorno de ejecución del pipeline de despliegue, la definición de las tareas del pipeline de despliegue y la determinación del momento de ejecución del pipeline de despliegue dentro del proceso de desarrollo de software.

