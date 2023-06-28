# ADR FAAS 0004. Ejecución sincrónica de comandos sobre otras funciones

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, sincrónica, comando, ejecución.

## Status

Accepted

References [ADR FAAS 0002. Orquestador](FAAS-0002-orquestador.md)

References [ADR MSG 0003. Eliminación de mensajes basura encolados](../../../messaging/doc/adr/MSG-0003-eliminacion-de-mensajes-basura-encolados.md)

References [ADR MSG 0004. Definición de timeouts y de reintentos demorados](../../../messaging/doc/adr/MSG-0004-definicion-de-timeouts-y-de-reintentos-demorados.md)

References [ADR MSG 0006. Creación de un procesador de mensajes basura encolados](../../../messaging/doc/adr/MSG-0006-creacion-de-un-procesador-de-mensajes-basura-encolados.md)

## Context

Al igual que con la tecnología de microservicios, se podría pensar en usar comunicaciones sincrónicas al ejecutar comandos sobre otras funciones. Es decir, establecer una comunicación entre dos o más componentes de forma simultánea, en donde la función que llama espera hasta que la otra función termina de realizar la tarea.

En modelos tradicionales (on premise o máquinas virtuales) el tiempo de uso de los recursos no tiene demasiado impacto en el costo total, ya que se paga un costo fijo por ser dueño de los recursos. Sin embargo, el uso de invocaciones sincrónicas provoca que algunos casos de uso no se adapten muy bien al modelo de uso de una "función como un servicio", ya que se paga por el tiempo de uso de los recursos.

Además, de que el costo total se ve impactado por el tiempo de uso, es importante considerar que al realizar varias invocaciones entre funciones podemos construir flujos orquestados de trabajo, los cuales no son adecuados de implementar en un "función como un servicio".

El uso de flujos sincrónicos presenta varios problemas en una arquitectura distribuida que emplea una "función como un servicio" como solución.

## Decision

No diseñaremos una "función como un servicio" que ejecute sincrónicamente comandos sobre otras funciones.

Esta decisión ayuda a evitar varios problemas que pueden surgir al emplear una arquitectura distribuida basada en "función como un servicio":

- Costo: Se paga por la duración de una invocación. Mayor tiempo de ejecución mayor pago.

- Manejo de errores: Las invocaciones anidadas requieren una mayor complejidad en el manejo de errores, ya que los errores generados en funciones más internas pueden provocar la necesidad de revertir la lógica ya realizada en las funciones superiores.

- Acoplamiento: Se establecen dependencias que afectan el tiempo de respuesta, ya que la respuesta total está condicionada por la función más lenta.

- Escalado: El acoplamiento de funciones lleva a tener que escalar todas las funciones por igual.

Tener funciones separadas que se invoquen asincrónicamente puede considerarse ineficiente. Sin embargo, debe recordarse que en una solución de "función como un servicio", los costos dependen del tiempo de su ejecución.

## Consequences

Usaremos una arquitectura asincrónica basada en colas para las invocaciones entre funciones o usaremos una Arquitectura Conducida por Eventos en donde cada función se desencadena por un evento de la función anterior en el flujo.

Emplearemos herramientas o servicios orientados y pensados en crear y en ejecutar flujos de trabajo complejos con múltiples tipos de fallas y lógica de reintento.

Necesitamos conocer si el proveedor de la nube nos brinda un servicio de bus de evento o de broker de mensajería que nos alivie los problemas asociados con la comunicación de eventos entre funciones.

Implementaremos mecanismos de reintentos y usaremos colas de dead-letter (cola de mensaje fallido) para invocaciones fallidas de funciones. Es importante conocer cual es la estrategia ofrecida por los proveedores de nube para tratar invocaciones de funciones asincrónicas fallidas.

La necesidad de usar eventos o colas para comunicaciones entre funciones puede llevar a complejizar el diseño, haciendo que no se vean los beneficios de la solución sin servidor. 
