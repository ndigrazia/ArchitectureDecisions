# ADR FAAS 0017. Servicio simple

## Keywords

faas, serverless, función, sin servidor, servicio, simple, caso uso.

## Status

Accepted

Referenced by [ADR FAAS 0012. Tareas en segundo plano](FAAS-0012-tareas-en-segundo-plano.md)

Referenced by [# ADR FAAS 0018. Envoltura temporal de una API HTTP](FAAS-0018-envoltura-temporal-de-una-api-http.md)

Referenced by [ADR FAAS 0001. Monolítica](FAAS-0001-monolitica.md)

## Context

Un servicio de software es aquel que realiza tareas como respuesta a eventos o a invocaciones de otros componentes de software. El resultado de la ejecución del servicio es la entrega de valor al negocio. 

Las soluciones tecnológicas usadas para poner en marcha las tareas o acciones del servicio varían de acuerdo a diferentes variables como la previsibilidad de su carga, la frecuencia de su uso, tamaño del servicio, caso de uso a ser resuelto, entre otras. 

La "función como un servicio" (FaaS) es una solución tecnológica moderna que permite a los desarrolladores construir servios o aplicaciones sin servidor. Es decir, sin la necesidad de poner foco en la infraestructura necesaria para su ejecución. Al igual que muchas soluciones tecnológicas, esta establece requisitos que al cumplirse potencian los beneficios del su uso y reducen sus desventajas.  

## Decision

Usaremos una "función como un servicio" para implementar servicios con cargas impredecibles, cuyo uso no es muy frecuente, con tiempo de ejecución reducido y con lógica no demasiado compleja.

Nuestro objetivo es que cada función realice una pequeña acción o tarea desencadenada generalmente por un evento.

El servicio desarrollado con una "función como un servicio" ofrece dos posibles escenarios para su invocación: ***Sincrónico*** o ***Asincrónico***. 

- Cuando el tipo de invocación es Sincrónica, necesitamos enfrentar el servicio con un API Gateway cuya función es dirigirle las solicitudes. Las solicitudes HTTP son considerados eventos en esta tecnología.

- Cuando el tipo de invocación es Asincrónica, requerimos enviar un evento para desencadenar el servicio. Además, es importante asegurarse de capturar las fallas para analizarlas y potencialmente reprocesarlas.

En general usaremos funciones en arquitecturas basada en eventos.

## Consequences

Requerimos el uso de una solución sin servidor cuando existe un procesamiento impredecible y poco frecuente. Sin embargo, es importante analizar los costos con el fin de determinar si el camino hacia una solución sin servicio es el más adecuado.

Requerimos descomponer la lógica de la aplicación en servicios individuales mas simples.

Requerimos reducir el tiempo de ejecución de los servicios implementados con una "función como un servicio".

La necesidad de eventos para comunicaciones entre funciones puede llevar a complejizar el diseño. 

Se reduce el costo de facturación.

Las soluciones sin servidores no requieren actividades de mantenimiento y de soporte.  

Difícil de depurar soluciones basadas en multiples funciones simples. 

Requerimos un API Gateway para invocaciones Sincrónicas.

Requerimos arquitecturas basadas en eventos con soluciones de bus de eventos (event bus).
