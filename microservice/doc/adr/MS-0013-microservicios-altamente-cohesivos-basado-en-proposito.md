# ADR MS 0013. Microservicios altamente cohesivos basado en propósito

Date: 2022-08-19

## Keywords

microservicio, cohesion, simple propósito, srp.

## Status

Superceded by [ADR MS 0014. Granularidad de los microservicios basada en propósito, transacciones u orquestación](MS-0014-granularidad-de-los-microservicios-basada-en-proposito-transacciones-u-orquestacion.md)

## Context

Los servicios que tienen muchas responsabilidades o que son responsables de realizar muchas funciones y muy diferentes, adolecen de los problemas de dificultad para su entendimiento, dificultad en el mantenimiento y son afectados frecuentemente por los cambios que puedan surgir.

## Decision

Desarrollamos y diseñamos microservicios altamente cohesivos estableciendo sus limites funcionales de acuerdo a su propósito en el dominio problema.

Idealmente, cada microservicio debería ser extremadamente cohesivo funcionalmente, contribuyendo con un comportamiento significativo a la aplicación general.

## Consequences

Requerimos diseñar e implementar microservicios con un solo propósito que no realicen gran cantidad de trabajo, aplicando el patrón de simple responsabilidad (SRP).
