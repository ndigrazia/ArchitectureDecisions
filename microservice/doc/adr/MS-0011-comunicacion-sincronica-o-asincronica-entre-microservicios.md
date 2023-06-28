# ADR MS 0011. Comunicación sincrónica o asincrónica entre microservicios

## Keywords

microservicio, comunicación, sincrónica, asincrónica, rest, amqp, mensajería.

## Status

Accepted

References [ADR MS 0010. Tolerancia a fallas en comunicación sincrónica](MS-0010-tolerancia-a-fallas-en-comunicacion-sincronica.md)

References [ADR MS 0012. Microservicios mínimamente acoplados](MS-0012-microservicios-minimamente-acoplados.md)

Referenced by [ADR MSG 0012. Determinación de estilos de comunicaciones asincrónicas](../../../messaging/doc/adr/MSG-0012-determinacion-de-estilos-de-comunicaciones-asincronicas.md)

## Context

El microservicio por sí solo no tiene sentido, es necesario que interactúe con otros para resolver un pedido o una necesidad. Cada microservicio es capaz de recibir mensajes, procesar datos y enviar mensajes hacia otros microservicios. 

Para poder establecer la comunicación, debe existir un estándar de comunicación que defina un conjunto de normas, acuerdos y recomendaciones técnicas que regulan la transmisión de mensajes entre los microservicios.

## Decision

Empleamos mecanismos de comunicación sincrónicos o asincrónicos para la comunicación entre los microservicios.

Los protocolos mas usados a la fecha en la comunicación entre los microservicios son: el protocolo sincrónico REST y el protocolo asincrónico AMQP (mensajería ligera).

Solicitamos poner en práctica la comunicación sincrónica mediante el protocolo REST.

Solicitamos poner en práctica la comunicación asincrónica mediante el protocolo AMQP.

La comunicación sincrónica es más conveniente en la mayoría de los casos, pero puede conducir a problemas de escalabilidad junto a otras características indeseables.

Si bien, favorecemos el uso de la comunicación asincrónica, ya que ayuda a mejorar el bajo acoplamiento y la extensibilidad, es importante tener presente que puede complicar el diseño y puede provocar dolor de cabeza a la hora de tratar las fallas y la sincronización de los datos.

Usamos comunicación sincrónica por defecto, y favorecemos el uso asíncrono cuando el diseño de la solución lo permita.

## Consequences

Requerimos, a la hora de implementar la comunicación sincrónica usando el protocolo REST, la definición de un artefacto (Interfaz API) que permita describir su contrato, documentar sus reglas y sus especificaciones. 

Solicitamos, a la hora de implementar la comunicación asincrónica usando el protocolo AMQP, precisar la estructura del mensaje que es enviado del emisor al receptor, acordar la instancia de cola de mensajes a utilizar y seleccionar el motor de mensajería (message broker).

