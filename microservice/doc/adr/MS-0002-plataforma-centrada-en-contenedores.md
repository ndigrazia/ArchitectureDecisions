# ADR MS 0002. Plataforma centrada en contenedores

## Keywords

microservicio, entorno, contenedor, elástica, plataforma, orquestación, fuente.

## Status

Accepted

Referenced by [ADR MS 0001. Reporte de estado de salud en microservicios](MS-0001-reporte-de-estado-de-salud-en-microservicios.md)

Referenced by [ADR MS 0006. Configuración elástica](MS-0006-configuracion-elastica.md), [ADR MS 0007. Reporte de métricas o telemetrías](MS-0007-reporte-de-metricas-o-telemetrias.md)

## Context

Debido a la naturaleza de simple propósito del microservicio, el tamaño del servicio es mucho más pequeño que en otras arquitecturas distribuidas, lo que ocasiona que su administración sea más compleja y más riesgosa. Disponer de un entorno de orquestación que permita gestionar los microservicios, eliminando muchos de los procesos manuales involucrados en la implementación, instanciación, ejecución, balanceo y escalabilidad de los mismos, ayuda a favorecer la estabilidad y la optimización de la infraestructura junto a la correcta ejecución de los servicios.

## Decision

Empleamos un entorno de orquestación centrado en contenedores para ejecutar los microservicios.

## Consequences

Requerimos el uso de un entorno de orquestación centrado en contenedores, configurar/programar el entorno de orquestación para realizar las actividades de instanciación, ejecución, balanceo y escalabilidad elástica de los microservicios.
