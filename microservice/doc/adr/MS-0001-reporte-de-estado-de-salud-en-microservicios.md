# ADR MS 0001. Reporte de estado de salud en microservicios

Date: 2022-08-16

## Keywords

microservicio, prueba de vida, prueba de aceptación, liveness, readiness, reporte, estado de salud.

## Status

Accepted

References [ADR MS 0002. Plataforma centrada en contenedores](MS-0002-plataforma-centrada-en-contenedores.md)

References [ADR MS 0003. Empaquetado del micro servicio como imagen de contenedor](MS-0003-empaquetado-del-microservicio-como-imagen-de-contenedor.md)

## Context

Muchos microservicios ejecutados durante largos períodos de tiempo pueden quedar en estados de falla que no les permiten recuperarse o les imposibilitan temporalmente atender el tráfico.  

La estabilidad de la plataforma de orquestación depende del estado de los microservicios desplegados dentro de la misma. Los microservicios necesitan reportar y/o publicar su estado de salud para indicar si están o no disponibles, tendiendo a mantener un ambiente estable y operativo.

## Decision

Publicamos y desarrollamos funciones de prueba de vida (Liveness) y de prueba de aceptación de pedidos (Readiness) en microservicios.

Las funciones de reporte de salud permiten a la plataforma de orquestación obtener conocimiento del estado de cada microservicio y así, conocer cuándo un microservicio se debe reiniciar o cuando está listo para comenzar a aceptar tráfico, garantizando un contexto de ejecución con condiciones conocidas.

Es importante la implementación de la prueba de vida al desplegar los microservicios en contenedores, ya que de lo contrario, la decisión de reiniciar el microservicio queda basada en el estado del proceso P1 (init process) padre de todos los procesos que corren en el contenedor, considerando que el microservicio funciona correctamente independientemente del estado de los procesos hijos que implementen la lógica de dicho servicio.

Por otro lado, la falta de implementación de la prueba de aceptación no permite identificar si el contenedor está listo para recibir tráfico o no. 

Una incorrecta implementación de la prueba de vida puede ocasionar fallas en cascadas y fluctuaciones durante la carga de los servicios en operaciones de auto escalamiento.

## Consequences

Requerimos el uso de frameworks o de librerías para implementar el reporte de estado de salud, desarrollo y publicación de la prueba de vida (Liveness) y la prueba de aceptación de pedidos (Readiness) en el microservicio y finalmente, empleo de una plataforma de orquestación que tome decisiones en función del estado de salud del microservicio.
