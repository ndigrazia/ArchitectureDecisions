# ADR MS 0007. Reporte de métricas o telemetrías

## Keywords

microservicio, métrica, telemetría, despliegue, soporte.

## Status

Accepted

References [ADR MS 0002. Plataforma centrada en contenedores](MS-0002-plataforma-centrada-en-contenedores.md)

## Context

Saber cómo están funcionando las instancias del microservicio es crucial para mantener la estabilidad del sistema. En producción, poder conocer la memoria del contenedor, el consumo de disco, el consumo de red, la JVM que están usando las instancias, cuántas veces se llama a un servicio, cuánto tiempo tardó en ejecutarse y varias otras métricas, ayudan al equipo de operaciones a administrar los servicios antes de que se vuelvan inestables. 

## Decision

Exponemos métricas o telemetrías que ayuden a administrar el microservicio, permitiendo detectar si el mismo se vuelve inestable en tiempo de ejecución.

Los microservicios deberán proporcionar en forma estándar sus métricas centrales, las cuales incluyen: Used Heap Memory, Max Heap Memory, Garbage Collection Count, entre otras. Como así también, las métricas del vendedor o de la aplicación que se consideren importante para el dominio problema.

Las telemetrías permiten conocer el estado de los microservicios antes de que se vuelvan inseguros, provocando la inestabilidad de todo el sistema. 

## Consequences

Requerimos el uso de alguna de las siguientes estrategias:

- Empleo de un service mesh: Una malla de servicios puede recopilar datos de telemetría de toda la red de microservicios y producir métricas consistentes en cada elemento de la red. La malla permite generar métricas del consumo de los recursos de los microservicios. Finalmente, los micro servicios solo deben enfocarse en brindar las métricas del vendedor y/o de la aplicación que se consideren mediante el uso de librerías.

- Utilización de librerías o de frameworks: El microservicio debe implementar funcionalidades para la recopilación de métricas centrales (tienen que ver con el estado de los recursos usados por el microservicio), métricas específicas del vendedor y métricas específicas de la aplicación (tienen que ver con indicadores propios del domino del negocio) mediante el uso de librerías.

En ambos casos se necesita un sistema de monitoreo donde se puedan analizar las métricas informadas. 

Se prefiere el empleo de una malla de servicio dado que es menos invasiva a la solución de librerías o de frameworks.
