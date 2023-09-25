# ADR CTR 0012. Uso de imágenes base con pequeñas huellas de software en ambientes productivos 

Date: 2023-09-21

## Keywords

containerizing, container, imagen, crear, construir, contenedor, huella, base, determinística, pequeña. 

## Status

Accepted

## Context

Cuando construimos imágenes de contenedores generalmente partimos de imágenes base desde las cuales iniciamos un proceso de modificación con el fin de obtener una nueva imagen. Estas imágenes base se componen de varias dependencias o herramientas de terceros las cuales representan sus huellas de software. Cuanto mas aumente las huellas de software en una imagen, mas posibilidades tenemos de un aumento en su tamaño, un incremento de sus vulnerabilidades y una menor resiliencia ante los cambios.

## Decision

Partimos de imágenes base con pequeñas huellas de software.

El uso de imágenes base con pequeñas huellas de software permite reducir el proceso de descarga y almacenamiento, disminuye los riesgos de vulnerabilidades y reduce los tiempos de construcción de las imágenes resultantes.

## Consequences

Requerimos que la imagen base sea una versión simplificada del sistema operativo, con pocas dependencias de librerías o herramientas de terceros y, con una versión estable y activa (con soporte a largo plazo) del ambiente de ejecución (runtime).
