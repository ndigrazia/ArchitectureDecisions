# ADR MS 0010. Tolerancia a fallas en comunicación sincrónica

Date: 2022-08-18

## Keywords

microservicio, comunicación, sincrónica, falla, tolerancia, reintento, timeout, fallback, circuit breaker.

## Status

Accepted

Referenced by [ADR MS 0011. Comunicación sincrónica o asincrónica entre microservicios](MS-0011-comunicacion-sincronica-o-asincronica-entre-microservicios.md)

## Context

Es sumamente importante, para aquellas aplicaciones que utilizan comunicación sincrónica, construir servicios con tolerancia a fallas. La tolerancia a fallas trata de aprovechar diferentes estrategias para guiar la ejecución y el resultado de cierta lógica, garantizando la estabilidad del servicio y de la aplicación en su conjunto.

## Decision

Ofrecemos estrategias de tolerancia a fallas en comunicaciones sincrónica de microservicios.  

Las políticas de reintento, timeouts, los Fallbacks y los Circuit Breaker son conceptos de esta área que establecen la lógica de tolerancia a falla que debe llevarse a cabo y el momento en ser ejecutada, ofreciendo un resultado alternativo cuando una ejecución no se completa con éxito.

El uso de estrategias de tolerancia a fallas garantiza la estabilidad de la aplicación.

## Consequences

Requerimos definir la estrategia de tolerancia a fallas para comunicaciones sincrónicas acordes al escenario a tratar, usando algunas de las siguientes políticas para su implementación:

- Disponer de un service mesh (malla de servicios) para implementar diferentes estrategias para tratar las fallas, previa configuración en dicho contexto.
  
- Uso de librerías o bibliotecas para lograr diferentes políticas de tolerancia a fallas como timeout, retry, bulkhead, Circuit-Breaker, Fallback, entre otras.

Se prefiere el empleo de una malla de servicio dado que es menos invasiva a la solución de librerías o de frameworks.
