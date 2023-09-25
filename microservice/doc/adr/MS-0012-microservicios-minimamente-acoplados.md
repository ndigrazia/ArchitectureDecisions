# ADR MS 0012. Microservicios mínimamente acoplados

Date: 2022-08-19

## Keywords

microservicio, comunicación, sincrónica, asincrónica, acoplamiento.

## Status

Accepted

Referenced by [ADR MS 0011. Comunicación sincrónica o asincrónica entre microservicios](MS-0011-comunicacion-sincronica-o-asincronica-entre-microservicios.md)

## Context

Los microservicios por sí solo no tienen sentido, necesitan estar comunicados con otros microservicios.

Los microservicios que están conectados a, tienen conocimiento de o confían en muchos otros microservicios, adolecen de los problemas de dificultad para su entendimiento de manera aislada, son complejos de reutilizar o probar, puesto que su uso requiere de la presencia adicional de otros microservicios, de los cuales este depende.  

Finalmente, una elevada dependencia de microservicios puede hacer que las modificaciones realizadas en algunos de sus vecinos afecten considerablemente a los servicios dependientes.

## Decision

Desarrollamos e implementamos microservicios con un acoplamiento bajo.

La comunicación sincrónica es más conveniente en la mayoría de los casos, pero puede conducir a una elevada dependencia de microservicios y provocar problemas de escalabilidad. Por tal motivo, diseñar microservicios con bajos niveles de acoplamiento aferente es sumamente importante.

Si bien, favorecemos el uso de la comunicación asincrónica, ya que es el mecanismo de comunicación que permite alcanzar mejores niveles de bajo acoplamiento comparado con la comunicación sincrónica, es importante tener presente que puede complicar el diseño y provocar dolor de cabeza a la hora de tratar las fallas y la sincronización de los datos.

Usamos comunicación sincrónica con bajos niveles de acoplamiento aferente, y favorecemos el uso asíncrono cuando el diseño de la solución lo permita.

## Consequences

Requerimos diseñar e implementar microservicios con mínimas dependencias y bajos niveles de acoplamiento aferente en comunicación sincrónica.

Solicitamos favorecer el uso de arquitecturas asincrónicas (Event-Driven Architecture) cuando el diseño de la solución lo permita.
