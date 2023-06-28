# ADR MSG 0010. Publicación de eventos de integración

## Keywords

messaging, message, asincrónica, mensaje, cola, evento

## Status

Accepted

## Context

Un evento es una notificación que produce un sistema al completar una transacción. En este documento nos referimos a eventos que son de alto nivel, importantes para el negocio, publicados para notificar a otros sistemas. El productor del evento no conoce cuales son los sistemas consumidores. Ejemplos de eventos pueden ser: "Cliente creado", "Orden creada", "pago efectuado", etc.

Al publicar un evento, el mensaje puede ser consumido por varios componentes interesados. Es necesario que los eventos puedan ser consumidos de forma eficiente.

## Decision

Publicaremos eventos de integración para reflejar cambios de estados en los objetos de dominios.

Los eventos deben poseer información del negocio que está representando, no debe estar dirigida a algún sistema particular, ni contener detalles propios de la implementación.

Los eventos no deben necesariamente contener toda la información, en muchos casos la información puede ser voluminosa afectando la performance de los sistemas consumidores. Además no todos los consumidores necesitan la misma información. Se debe enviar la información básica del evento que en general sea util a todos los consumidores y referencias para el caso que el consumidor necesite completar con mas información.

Es necesario definir una estructura básica para eventos de negocio que contenga la información común a todos los eventos, de forma que sea posible realizar una traza del mensaje, por ejemplo con información del sistema origen, el momento de la creación y el id del evento.

Los eventos expuestos a otros sistemas comerciales son notificaciones de alto nivel que son importantes para el negocio, son conocidas y definidas por grupos interdiciplinarios de analistas, usuarios y desarrolladores.

## Consequences

Siempre es complicado el balance del esfuerzo entre la facilidad de generar un evento con toda la información y la complicación de utilizar varias integraciones para completar la información de un evento.

La cuestión es no acoplar consumidores a una estructura mal formada o muy propensa a cambios. Contar solamente con la información básica nos permite mitigar este riesgo. 
