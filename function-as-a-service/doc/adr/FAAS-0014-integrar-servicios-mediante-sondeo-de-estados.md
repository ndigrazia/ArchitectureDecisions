# ADR FAAS 0014. Integrar servicios mediante sondeo de estados

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, evento, integración, sondeo, estado, caso uso.

## Status

Accepted

## Context

Un sistema distribuido es cualquier sistema en donde sus componentes están separados pero no aislados, ya que se comunican unos con otros mediante una red.

Generalmente, la comunicación entre los componentes de un sistema distribuido es asincrónica, lo que significa invocar una tarea y no quedar bloqueado a la espera de un resultado. En las comunicaciones asincrónicas se intercambian mensajes o eventos entre los componentes del sistema distribuido.

Pero, ¿Qué sucede cuando uno de los componentes no tiene la capacidad de integrarse con el resto de los componentes del sistema? ¿Como comunicar componentes que no pueden generar eventos nativamente? Podemos realizar repetidos sondeos (polling) al servicio para conocer su estado y de esta manera, comunicar al resto del sistema sus cambios.  

Estas solicitudes o sondeos pueden ser realizados con funciones o con contenedores.

## Decision

Usaremos una "función como un servicio" para sondear el estado de un componente y así, adaptar dos componentes cuando no hay una integración nativa entre ellos. 

Usaremos funciones para implementar sondeos dada sus características periódicas, ya que el uso de contenedores involucraría el pago por sus horas de disponibilidad independientemente de su uso.

Configuramos la invocación periódica de una función en el programador de trabajos (scheduler). La función tendrá la lógica para sondear el servicio y creará eventos para informar los cambios en su estado a las partes del sistema que estén interesadas en conocerlo.

## Consequences

Requerimos un programador de trabajos para realizar las invocaciones periódicas a la función.

Requerimos una plataforma de ejecución de la solución sin servidor.

Usaremos una arquitectura asincrónica basada en eventos donde la función desencadena un evento para informar el cambio de estado del sistema sondeado.

Necesitamos conocer si el proveedor de la nube nos brinda un servicio de bus de evento o de broker de mensajería que nos alivie los problemas asociados con la comunicación de eventos.

Requerimos lógica de sondeo con alta performance y alta disponibilidad.

El uso de una arquitectura asincrónica puede complejizar el diseño.
