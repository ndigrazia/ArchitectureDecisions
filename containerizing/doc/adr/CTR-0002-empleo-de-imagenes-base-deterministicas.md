# ADR CTR 0002. Empleo de imágenes base determinísticas

## Keywords

containerizing, container, imagen, crear, construir, contenedor, etiqueta, base, versión, determinística. 

## Status

Accepted

## Context

El proceso de construcción de imágenes de contenedores inicia generalmente con imágenes base sobre la cuales realizamos ciertas acciones que dan como resultado imágenes finales adaptadas a nuestras necesidades. Pero, ¿Cómo garantizamos que estamos partiendo de una imagen consistente y determinística? Es decir, que nuestro proceso de construcción es un proceso que parte de una imagen conocida que confía en que la imagen no cambia.

Las imágenes de contenedores son referenciadas mediante un identificador hash SHA-256 (digest) que garantiza que nuestra imagen no ha cambiado. Sin embargo, este identificador no es agradable al desarrollador que lo observa, ya que de primera vista no puede identificar ciertas características de la imagen (S.O, runtime, herramientas, etc). Además, herramientas (como los analizadores de vulnerabilidades) que operan con la imagen pueden carecer de la posibilidad de interpretarlo.

Como alternativa al identificador hash podemos usar etiquetas para referenciar a las imágenes base. Sin embargo, este mecanismo  no garantiza que la imagen base usada en el proceso sea la misma en sus reiteradas ejecuciones.

## Decision

Empleamos imágenes base determinísticas, versionadas mediante etiquetas, en aquellos procesos de construcción de imágenes de contenedor que utilizan una imagen base como punto de partida.

Si bien es mutable y podría usarse la misma etiqueta para referenciar a diferentes imágenes, la utilización de un adecuado mecanismo de versionado (por ejemplo versionado semántico) permite que las actualizaciones de seguridad u otras actualizaciones, se materialicen en una nueva versión, por lo que es seguro asumir construcciones de imágenes consistentes y determinísticas.

## Consequences

Requerimos el uso de imágenes base determinísticas, versionadas mediante etiquetas.

Requerimos un mecanismo de versionado claro y ampliamente conocido por todos los equipos de desarrollo, ya que el uso de etiquetas no garantiza una referencia única de las imágenes.

Finalmente, requerimos el empleo de un identificador hash SHA-256 (digest) en el caso que se requiera garantizar fehaciente que la imagen no ha cambiado.
