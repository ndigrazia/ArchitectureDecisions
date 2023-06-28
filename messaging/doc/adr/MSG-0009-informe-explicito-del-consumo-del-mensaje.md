# ADR MSG 0009. Informe explicito del consumo del mensaje

## Keywords

messaging, message, asincrónica, mensaje, cola, consumo.

## Status

Accepted

Referenced by [ADR MSG 0008. Almacenamiento persistente y envió sincrónico del mensaje](MSG-0008-almacenamiento-persistente-y-envio-sincronico-del-mensaje.md)

## Context

La pérdida de datos siempre es una preocupación en comunicaciones asincrónicas, ya que hay muchos lugares donde puede ocurrir dicha pérdida.

Por pérdida de datos nos referimos a un mensaje que nunca llega a su destino final.

Si bien la perdida de mensajes en una comunicación asincrónicas puede ocurrir en tres áreas distintas, dos de ellas, están directamente relacionada con los puntos de comunicación del mensaje.

La primera es tratada en el documento de referencia de [Almacenamiento persistente y envió sincrónico del mensaje](#status)

La segunda ocurre cuando cuando el consumidor rompe o falla antes de procesar el mensaje.

Existen técnicas básicas de mensajería para mitigar dicha perdida de datos.

## Decision

Empleamos la técnica básica de mensajería llamada modo de reconocimiento de cliente (client acknowledge mode) para confirmar que el mensaje fue procesado por el consumidor.

De forma predeterminada, cuando se retira el mensaje de la cola, se envía inmediatamente al consumidor para su procesamiento, eliminado dicho mensaje de la cola (auto acknowledge mode).

El modo de reconocimiento de cliente mantiene el mensaje en la cola, indicando su consumidor para que ningún otro consumidor pueda procesar el mensaje. Con este modo, si el consumidor falla, el mensaje aún se conserva en la cola, impidiendo su perdida y permitiendo su posterior procesamiento.

## Consequences

Requerimos activar el modo de reconocimiento de cliente e informar explícitamente que el mensaje fue procesado por el consumidor.
