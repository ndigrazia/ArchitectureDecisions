# ADR MESH 0002. Envío de headers para trazabilidad

Date: 2022-10-04

## Keywords

mesh, sidecar, malla de servicios, trazabilidad.

## Status

Accepted

References [ADR MS 0006. Configuración elástica](../../../microservice/doc/adr/MS-0006-configuracion-elastica.md)

## Context

Los microservicios deben reenviar los headers requeridos para que la malla de servicios pueda registrar la traza de las invocaciones.

## Decision

Enviaremos headers de trazabilidad en la cadena de invocaciones de los microsevicios que componen la malla de servicios.

Los headers de trazabilidad son necesarios para poder visualizar la cadena de invocaciones de una forma amigable con la herramienta de visualización disponible en nuestra malla de servicios y así, poder determinar los casos en donde la invocación tuvo demoras u otros problemas.

Para poder realizar la trazabilidad de la invocaciones, necesitamos enviar los siguientes headers en las invocaciones de los servicios que forman la malla de servicios:

    - x-request-id
    - x-b3-traceid
    - x-b3-spanid
    - x-b3-parentspanid
    - x-b3-sampled
    - x-b3-flags
    - b3

Modificamos los headers de trazabilidad sin necesidad de construir o de empaquetar nuevamente el servicio, usando la estrategia de configuración elástica.

## Consequences

La lógica del microservicio debe evaluar: si los headers llegan en la invocación del microservicio, este lo debe enviar en las invocaciones que realice.
