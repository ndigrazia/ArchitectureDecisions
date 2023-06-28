# ADR MSG 0001. Actualizaciones asincrónicas mediante mensajes de comandos

## Keywords

messaging, message, asincrónica, comando, mensaje, cola.

## Status

Accepted

## Context

Las aplicaciones que realizan actualizaciones sincrónicas suelen responder con invocaciones a la capa de servicio. En este enfoque todas las llamadas del servicio deben completarse antes de retornar una respuesta. Este modelo también requiere que la escalabilidad y la disponibilidad de la capa de servicio coincidan e incluso, superen a los requerimientos de la capa de presentación, que en algunos casos puede ser difícil de determinar como por ejemplo, cuando se usan servicios de terceros para resolver los pedidos. También, puede ocurrir que un servicio no sea confiable o que su procesamiento sea lento, llevando a arruinar la experiencia del usuario y a afectar negativamente la escalabilidad. 

## Decision

Favorecemos el envío de mensajes de comandos asincrónicos para actualizar datos.

El uso de colas y los mensajes que indiquen la actividad a realizar, permiten desacoplar el cliente del servicio encargado de resolver la solicitud. Esta separación lleva a que el cliente no tenga que esperar por una respuesta, garantizando tiempos de retorno (responsiveness) consistentemente rápidos.

## Consequences

Requerimos acordar la estructura del mensaje de comando que es enviado del emisor al receptor, definir la instancia de cola de mensajes a utilizar y desarrollar el componente encargado de actualizar el dato en la base de datos (data pump).
