# ADR MSG 0008. Almacenamiento persistente y envió sincrónico del mensaje

Date: 2022-08-30

## Keywords

messaging, message, asincrónica, mensaje, cola, persistencia.

## Status

Accepted

References [ADR MSG 0004. Definición de timeouts y de reintentos demorados](MSG-0004-definicion-de-timeouts-y-de-reintentos-demorados.md)

References [ADR MSG 0009. Informe explicito del consumo del mensaje](MSG-0009-informe-explicito-del-consumo-del-mensaje.md)

## Context

La pérdida de datos siempre es una preocupación en comunicaciones asincrónicas, ya que hay muchos lugares donde puede ocurrir dicha pérdida.

Por pérdida de datos nos referimos a un mensaje que nunca llega a su destino final.

Si bien la perdida de mensajes en una comunicación asincrónicas puede ocurrir en tres áreas distintas, dos de ellas, están directamente relacionada con los puntos de comunicación del mensaje.

La primera ocurre cuando el mensaje nunca llega a la cola desde el productor o incluso si lo hace, el intermediario (Broker) se cae antes de que el mensaje pueda ser consumido o almacenado en un almacenamiento físico.

La segunda es tratada en el documento de referencia de [Informe explicito del consumo del mensaje](#status)

Existen técnicas básicas de mensajería para mitigar dicha perdida de datos.

## Decision

Usamos mecanismos de almacenamiento persistente en colas de mensajes.

Enviamos sincrónicamente el mensaje desde el productor al intermediario y quedamos a la espera de su aceptación. 

Cuando el intermediario de mensajes recibe el mensaje, no solo lo almacena en la memoria para una recuperación rápida, sino también lo persiste en algún tipo de almacén de datos físicos. Si el intermediario deja de funcionar, el mensaje queda almacenado físicamente para su posterior procesamiento, cuando el intermediario vuelve a funcionar.

El productor espera hasta que el intermediario ha reconocido que el mensaje ha sido persistido.

## Consequences

Requerimos activar el mecanismo de almacenamiento persistente en la cola de mensajes y enviar sincrónicamente cada mensaje a la cola.

Es importante definir el tiempo de espera del productor y el accionar en casos de no contar con una respuesta. Para mas detalle ver el documento de referencia de [Definición de timeouts y de reintentos demorados](#status)