# ADR MS 0015. Adecuado nivel de complejidad para el dominio problema

Date: 2022-08-19

## Keywords

microservicio, complejidad ciclomática, soporte.

## Status

Accepted

## Context

Las aplicaciones construidas con códigos demasiados complejos conducen a algoritmos difíciles de interpretar y de mantener, dañando varias características deseables en el código fuente, como la modularidad, capacidad de prueba, capacidad de despliegue, etc.

## Decision

Construimos microservicios con niveles de complejidad adecuados al dominio de problema que se pretende atacar.

## Consequences

Requerimos desarrollar microservicios con las siguientes complejidades ciclomáticas:

- Domino simple: 1-4 de complejidad ciclomática.
- Domino moderado: 5-10 de complejidad ciclomática.
- Domino complejo: 10-15 de complejidad ciclomática.

En el caso del dominio complejo, es importante evaluar la posibilidad de descomponer la lógica del servicio, ya que en general el valor aceptado en la industria es 10 y, cualquier valor mayor a este se puede considerar un valor riesgoso.
