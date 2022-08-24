# ADR MS 0014. Granularidad de los microservicios basada en propósito, transacciones o coreografía.

Date: 2022-08-19

## Keywords

microservicio, cohesion, simple propósito, contexto transaccional, coreografía, srp.

## Status

Accepted

Supercedes [ADR MS 0013. Microservicios altamente cohesivos basado en propósito](MS-0013-microservicios-altamente-cohesivos-basado-en-proposito.md)

## Context

Generalmente, los desarrolladores buscan encontrar la correcta granularidad o los adecuados límites funcionales en los servicios. A menudo, durante el proceso de desarrollo del servicio cometen el error de hacer sus servicios demasiado pequeños, lo que les obliga a construir vínculos de comunicación entre los servicios aumentando su acoplamiento o, incurren en el error de asignar muchas responsabilidades y muy diferentes a los servicios, lo que adolece de problemas en su entendimiento y dificultad en su mantenimiento.

Encontrar la adecuada granularidad o los límites funcionales en los servicios es sumamente importante para el éxito de la aplicación.

## Decision

Desarrollamos y diseñamos microservicios altamente cohesivos estableciendo sus límites funcionales de acuerdo a su propósito en el dominio problema o contexto transaccional o su función coreográfica.

## Consequences

Requerimos diseñar e implementar microservicios estableciendo su granularidad de acuerdo a alguno de los siguientes criterios:

- Propósito: Construir microservicios contribuyendo con un comportamiento significativo a la aplicación general, con un solo propósito, que no realicen gran cantidad de trabajo, aplicando el patrón de simple responsabilidad (SRP).

- Contexto transaccional: Construir microservicios orientados a un contexto transaccional, estableciendo la granularidad o el límite del servicio entre las entidades que necesitan cooperar para alcanzar el objetivo. Debido a que las transacciones causan problemas en las arquitecturas distribuidas, es mejor diseñar el sistema para evitarlas, estableciendo los límites de los servicios entre las entidades que conforman la transacción.

- Coreográfica: Construir microservicios más grande para evitar la comunicación entre un conjunto de microservicios aun cuando los microservicios ofrezcan un excelente aislamiento de dominio, pero requieran de una amplia comunicación entre ellos para funcionar.
  