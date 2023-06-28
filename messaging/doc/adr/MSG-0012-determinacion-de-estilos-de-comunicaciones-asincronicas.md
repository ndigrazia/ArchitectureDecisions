# ADR MSG 0012. Determinación de estilos de comunicaciones asincrónicas

## Keywords

messaging, integración, message, asincrónica, mensaje, cola, evento, comunicación.

## Status

Accepted

References [ADR MESH 0001. Uso de sidecar para acoplamiento operativo](../../../mesh/doc/adr/MESH-0001-uso-de-sidecar-para-acoplamiento-operativo.md)

References [ADR MS 0017. Arquitectura hexagonal para el desarrollo de microservicios](../../../microservice/doc/adr/MS-0017-arquitectura-hexagonal-para-el-desarrollo-de-microservicios.md)

## Context

En la comunicación asincrónica los servicios se comunican intercambiando mensajes de forma asíncrona. 

El servicio emisor envía un mensaje usando un intermediario de mensajes (otra opción es utilizar una arquitectura sin intermediarios), sin quedar bloqueado a la espera de una respuesta, ya que asume que dicha respuesta no se recibirá inmediatamente. En esta estrategia de comunicación, los mensajes se intercambian a través de canales de mensajes. Es decir, un emisor escribe un mensaje en un canal y el receptor lee los mensajes de ese canal.

Existen dos tipos de canales:

- Punto a punto: Se entrega un mensaje exactamente a uno de los consumidores que está leyendo del canal.
- Publicación-suscripción: Se entrega cada mensaje a todos los consumidores suscriptos al canal.

Un mensaje se compone de un encabezado y un cuerpo.

El encabezado es una colección de pares de nombre y valor que describen el mensaje. El cuerpo del mensaje son los datos que se envían en formato de texto o de binario. Hay varios tipos diferentes de mensajes:

- Documento: Contiene solo datos que es interpretado por el receptor.
- Comando: Especifica la operación a invocar y sus parámetros.
- Evento:  Indica que ha ocurrido un cambio de estado del sistema.

## Decision

Implementaremos los siguientes estilos de comunicaciones asincrónicas en integración de servicios: ASYNCHRONOUS REQUEST/RESPONSE, ONE-WAY NOTIFICATIONS, PUBLISH/SUBSCRIBE y PUBLISH/ASYNC RESPONSES. 

Cada servicio que use una comunicación asíncrona utilizará una o más de estas técnicas de implementación de acuerdo al escenario que plantee resolver.

ASYNCHRONOUS REQUEST/RESPONSE

Cuando un cliente y un servicio interactúan mediante solicitud/respuesta asincrónica, el cliente envía un comando de mensaje a un canal "Punto a Punto" propiedad del servicio receptor, especificando la operación a realizar y sus parámetros. El servicio receptor procesa las solicitudes desde el canal y envía un mensaje de respuesta (Documento), que contiene el resultado, a un canal "Punto a Punto" propiedad del cliente.

En este intercambio de mensajes, el cliente debe indicarle al servicio receptor dónde enviar su mensaje de respuesta y, el receptor debe indicar a que mensaje corresponde dicha respuesta. Afortunadamente, estos dos problemas se resuelven mediante encabezados especiales existentes en los mensajes intercambiados. El cliente envía el encabezado "Message ID" y "Reply Channel" para indicar el id del mensaje y el canal de respuesta. El servicio receptor envia la respuesta al canal indicado en el encabezado "Reply Channel" y el encabezado "Correlation ID" con el valor del ID del mensaje que está respondiendo. El cliente usa la identificación de correlación para hacer coincidir el mensaje de respuesta con la solicitud. 

ONE-WAY NOTIFICATIONS

La implementación de notificaciones unidireccionales es sencilla. El cliente envía un mensaje, normalmente un mensaje de comando, a un canal "Punto a Punto" propiedad del servicio receptor. El servicio lee y procesa el mensaje. No devuelve una respuesta.

PUBLISH/SUBSCRIBE

Este tipo de comunicación es utilizada por los servicios para publicar eventos de dominio, que representan cambios en los objetos de dominio. Un cliente publica un mensaje en un canal de "Publicación-suscripción" que es leído por múltiples consumidores. Aquellos consumidores que están interesados en los eventos de un objeto de dominio en particular solo tienen que suscribirse al canal apropiado.

PUBLISH/ASYNC RESPONSES

El estilo de interacción es implementado mediante la combinación de elementos de PUBLISH/SUBSCRIBE y ASYNCHRONOUS REQUEST/RESPONSE. Un cliente publica un mensaje con el encabezado "Reply Channel" en un canal de "Publicación-suscripción". Un consumidor escribe un mensaje de respuesta conteniendo el "Correlation ID" en el canal indicado en el encabezado "Reply Channel". El cliente recopila todas las respuestas utilizando el "Correlation ID".

## Consequences

El uso de comunicación asincrónica facilita el desacoplamiento de los servicios permitiendo mejorar sus tiempos de respuestas y su escalamiento individual. Estas ventajas son obtenidas a costa de complejizar la solución. 

Una estrategia de comunicación asincrónica tiene que considerar dos partes: su infraestructura y, la lógica, que el servicio empleará, para el envió y la recepción de mensajes.

INFRAESTRUCTURA:

Requerimos disponer de un intermediario de mensajes (broker) con configuraciones que reflejen los requerimientos del caso de negocio, determinar el escenario que se plantea resolver y de acuerdo a esto, definir el tipo canal de comunicación a usar (Punto a punto o Publicación-suscripción).

LÓGICA DE ENVIÓ DE MENSAJES:

Requerimos disponer de uno o más adaptadores de entradas (Inbound adapter) que manejen solicitudes desde el exterior al servicio. Y de manera similar, uno o más adaptadores de salidas (Outbound adapter) que manejen solicitudes desde el servicio hacia el exterior. Cada uno de estos adaptadores disponen de lógica, basada en librerías especificas de la infraestructura, para el envió y la recepción de mensajes. Los adaptadores implementarán interfaces que permiten que la lógica del negocio quede separada de la lógica de acceso a la infraestructura.

Los adaptadores son componentes de la arquitectura hexagonal.

Otra alternativa es encapsular la lógica del acceso a la infraestructura mediante el uso de un componente de sidecar.
