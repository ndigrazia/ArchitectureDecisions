# ADR FAAS 0012. Tareas en segundo plano

Date: 2023-03-14

## Keywords

faas, serverless, función, sin servidor, servicio, tarea, segundo plano, caso uso.

## Status

Accepted

References [ADR FAAS 0008. Patrones de carga predecibles](FAAS-0008-patrones-de-carga-predecibles.md)

References [ADR FAAS 0017. Servicio simple](FAAS-0017-servicio-simple.md)

## Context

La mayoría de las aplicaciones de software se componen de tareas interactivas y/o tareas en segundo plano. Las tareas interactivas son desencadenadas por el usuario al interactuar con la interfaz de la aplicación. Estas tareas requieren un tiempo de respuesta corto. En cambio, las tareas de segundo plano son operaciones de larga duración que se desencadenan manualmente o automáticamente sin interacción del usuario. 

Si bien, las tareas de segundo plano no requieren de la participación del usuario, puede ocurrir la necesidad de ejecutar una tarea de larga duración desde una solicitud del usuario. En estos escenarios podemos emplear una "función como un servicio" para ejecutar dicha tarea si se reúnen las condiciones de frecuencia de uso y de previsibilidad de su carga.

## Decision

Usaremos una "función como un servicio" para realizar tareas de segundo plano desencadenadas ocasionalmente o de manera impredecible.

A pesar de que las tareas de segundo plano gozan de un tiempo mayor de respuesta con respecto a las tareas interactivas, es importante conocer el tiempo máximo de ejecución establecido por la plataforma, ya que si se supera ese tiempo se cancelará la ejecución de la "función como un servicio".

Descomponemos o desacoplamos la lógica de tratamiento usada en la "función como un servicio" si consideramos excesiva la duración de la tarea de segundo plano. La duración de la tarea impacta en el costo facturado.

Conectamos una "función como un servicio" detrás de un API Gateway para atender las peticiones de ejecución de tareas de segundo plano, retornando el código de respuesta adecuado y almacenando dichas solicitudes en una cola de mensajería. Luego, como respuesta a los mensajes almacenados, invocaremos a la función que contiene la lógica de la tarea de segundo plano.

Requerimos el almacenamiento y el procesamiento de los mensajes fallidos. Esta acción puede ser realizada mediante una "función como un servicio".

Considerar implementar con servicios con cargas impredecibles y cuyo uso no es muy frecuente.

Usar funciones en tareas en segundo plano que no se verán afectadas por arranques en frio.

## Consequences

Requerimos el uso de un bróker de mensajería (message broker) y colas de mensajería funcionando en alta disponibilidad.

Requerimos el empleo de un API Gateway en donde las peticiones serán dirigidas y sometidas a evaluaciones de seguridad.

Requerimos una plataforma de ejecución de la solución sin servidor.

El uso de una cola de mensajería (buffer) ayuda a hacer más resiliente a la solución, ya que permite volver a tratar una petición ante una falla pero, como contrapartida, el diseño se vuelve más complejo.

El tiempo total de ejecución (inicio + procesamiento) de una tarea en segundo plano esta afectado por el tiempo de arranque de la función que lo implementa (tiempo de arranque en frio). 
