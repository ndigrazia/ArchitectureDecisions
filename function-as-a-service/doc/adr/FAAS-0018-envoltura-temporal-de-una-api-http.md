# ADR FAAS 0018. Envoltura temporal de una API HTTP

## Keywords

faas, serverless, función, sin servidor, servicio, migración, api, http.

## Status

Accepted

References [ADR FAAS 0017. Servicio simple](FAAS-0017-servicio-simple.md)

## Context

A medida que el negocio evoluciona, los servicios que fueron creados a partir de este comienzan a verse impactados por sus cambios, dando surgimiento, entre otras cosas, a nuevas interfaces de programación de aplicaciones (API).

Llevar adelante el reemplazo por completo de una API por otra puede ser una enorme tarea sujeta a muchas complicaciones, dado que no solo se requiere el diseño de la nueva interfaz sino que también, la implementación de los nuevos servicios que le dan soporte.

A menudo, una migración gradual es una mejor alternativa. Es decir, diseñamos la nueva interfaz manteniendo los servicios anteriores. Pero,
¿Cómo envolvemos una API HTTP temporalmente otra API HTTP mientras se construye un servicio diferente?

## Decision

Implementaremos o diseñaremos una "función como un servicio" para envolver temporalmente una API HTTP mientras se construye el nuevo servicio. 

Considerar implementar con servicios con cargas impredecibles y cuyo uso no es muy frecuente.

Configuramos un API Gateway para que reciba las nuevas solicitudes y las dirija a una función que pueda validar y/o modificar la solicitud, enviándola al punto de origen (endpoint) para luego, modificar la respuesta antes de devolverla al solicitante original. Una vez implementada la versión de toda la API, podemos cambiar la invocación hacia los servicios finales.

## Consequences

Requerimos una plataforma de ejecución de la solución sin servidor.

Requerimos una solución de API Gateway.

Requerimos lógica de adaptación de API HTTP con alta performance y alta disponibilidad.
