# ADR FAAS 0016. Abanico (Fanning out)

## Keywords

faas, serverless, función, sin servidor, servicio, fan out, fanning out, caso uso.

## Status

Accepted

## Context

Muchos casos de uso requieren que un componente cree múltiples tareas adicionales, ya sea porque su lógica es  demasiado compleja y debe ser descompuesta en servicios individuales o porque lleva demasiado tiempo de ejecución.

Varias plataformas en la nube limitan el uso de las funciones a ciertos minutos de ejecución, por lo tanto, muchas tareas implementadas con funciones, que hacen uso intensivos en tiempo, pueden superar fácilmente esta limitación cancelando su ejecución.

## Decision

Implementaremos o diseñaremos una "función como un servicio" que descomponga la complejidad del trabajo en una series de servicios o tareas mas sencillas implementadas mediante otras funciones mas simples.

Usaremos eventos, dado que es una de las capacidades naturales de esta tecnología, para invocar las funciones mas sencillas, logrando desconectar la función de llamada del resto de las funciones de tarea.

Requerimos un repositorio común para los casos que necesiten agregar los resultados de los trabajos más pequeños, ya que las funciones mas simples están desacopladas de la función principal. Además, junto al resultado de cada tarea, solicitamos un Identificador de Unidad de Trabajo y un Identificador de Tarea. 

Requerimos el almacenamiento y el procesamiento de los mensajes fallidos.

## Consequences

Requerimos el uso de un bróker de mensajería (message broker) y colas de mensajería funcionando en alta disponibilidad.

Requerimos una plataforma de ejecución de la solución sin servidor.

El uso de una solución de fanning out en algunos casos puede considerarse un anti-patron.

La necesidad de usar eventos para comunicaciones entre funciones puede llevar a complejizar el diseño.
