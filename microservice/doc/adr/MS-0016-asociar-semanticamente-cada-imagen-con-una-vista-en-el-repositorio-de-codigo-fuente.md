# ADR MS 0016. Asociar semánticamente cada imagen con una vista en el repositorio de código fuente

## Keywords

microservicio, repositorio, fuente, código, soporte.

## Status

Accepted

References [ADR MS 0003. Empaquetado del micro servicio como imagen de contenedor](MS-0003-empaquetado-del-microservicio-como-imagen-de-contenedor.md)

References [ADR MS 0005. Único repositorio de fuentes](MS-0005-unico-repositorio-de-fuentes.md)

## Context

Los sistemas de control de versiones nos permiten almacenar las fuentes de las aplicaciones en repositorios y nos ayudan a garantizar la trazabilidad de sus cambios.

Al momento de empaquetar la imagen de la aplicación en un contenedor, se garantiza un entorno consistente que va desde desarrollo hasta producción. Cada cambio o fix que requiera la imagen en producción, impactará en sus fuentes, pues la imagen es inmutable. 

Las etiquetas son apuntadores que permiten referenciar un punto en el historial del repositorio asociado a una imagen determinada. Por medio del uso de etiquetas se puede obtener la foto del repositorio al momento de crear la imagen de contenedor, permitiendo acceder a su código fuente original sin ninguna otra modificación.

 # Decision

Asociamos semánticamente la imagen de contenedor con su estado en el repositorio de código fuente.

Una foto correcta del código fuente es indispensable para poder dar soporte y dar mantenimiento a la versión de la imagen de contenedor.

## Consequences

Requerimos el uso de un sistema de control de versiones, crear un repositorio de código fuente para el microservicio, generar una etiqueta (tag) en el repositorio de código fuente por cada imagen de contenedor construida.
