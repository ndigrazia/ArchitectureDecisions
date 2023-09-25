# ADR CTR 0001. Exclusión de imágenes base basadas en el proyecto Linux Alpine

## Keywords

containerizing, container, imagen, crear, construir, contenedor, base. 

## Status

Accepted

## Context

Generalmente cuando construimos imágenes de contenedores partimos de imágenes base desde las cuales iniciamos un proceso de modificación con el fin de obtener una nueva imagen que cumplimente todas las necesidades requeridas. Existen múltiples opciones de imágenes base, las cuales varían de acuerdo a: distribución o versión del sistema operativo, tipo o versión del runtime,  herramientas disponibles, soporte otorgado, etc. 

Hay, dentro del universo de imágenes base disponibles, algunas imágenes basadas en proyectos experimentales o proyectos en fases de prueba que debemos evitar cuando construimos imágenes de contenedores.

## Decision

Evitamos emplear imágenes base basadas en el proyecto Linux Alpine para la construcción de imágenes de contenedores.

Las imágenes base basadas en el proyecto Alpine al poseer menores dependencias de componentes de software permiten obtener imágenes resultantes con tamaños reducidos y con menor número de vulnerabilidades. Estas propiedades las hacen atractivas de ser seleccionadas. Sin embargo, el proyecto Alpine usa una implementación distinta (musl) de la librería de acceso a los recursos del Sistema Operativo (Librería estándar C). Esta diferencia la distingue de la implementación por defecto (glibc) usada por el resto de las distribuciones de Linux, haciéndola no adecuada para toda clase de proyectos de software, ya que, en algunos casos, se han presentado problemas de performance o errores funcionales.

Además, muchos escáneres de vulnerabilidades de seguridad no pueden detectar fácilmente las vulnerabilidades en imágenes basadas en el proyecto Alpine.

## Consequences

Requerimos no seleccionar imágenes base basadas en el proyecto Linux Apline para la construcción de imágenes de contenedores.
