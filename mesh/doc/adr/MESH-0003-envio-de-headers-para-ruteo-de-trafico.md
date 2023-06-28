# ADR MESH 0003. Envío de headers para ruteo de tráfico

## Keywords

mesh, sidecar, malla de servicios, trazabilidad.

## Status

Accepted

References [ADR MS 0006. Configuración elástica](../../../microservice/doc/adr/MS-0006-configuracion-elastica.md)

## Context

Es necesario disponer de headers que deben reenviarse en las invocaciones a microservicios para que la malla de servicios pueda tomar
acciones según su contenido.

## Decision

Usaremos headers para rutear el trafico de las invocaciones de los servicios según su contenido.

Los headers nos sirven para por ejemplo: rutear el trafico a distintas versiones de un microservicio según, el usuario que esté invocando, o el ambiente en donde se esté ejecutando, o elevar el nivel de log según un numero de ani, o enviar flags para que un componente tenga un comportamiento diferente.

Los headers a modo de ejemplo podrían ser:

    - x-tef-user (usuario de la aplicación).
    - x-tef-product-id (identificador de producto, puede ser el ani).
    - x-tef-log  (indica si se loguea esta invocación, ejemplo ”x-teflog: yes”).
    - x-tef-flags (uso general, ejemplo: ”x-tef-flags: v1,feature2=yes”).
    - x-tef-env (código de ambiente en el cual se est´a ejecutando).

Modificamos los headers de ruteo de contenido sin necesidad de construir o de empaquetar nuevamente el servicio, usando la estrategia de configuración elástica.

## Consequences

Los microservicios deben reenviar todos los headers que comienzan con ”x-tef-” para que se puedan implementar este tipo de funcionalidades.
