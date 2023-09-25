# ADR CTR 0010. Utilización de imágenes provenientes de fuentes confiables

Date: 2023-09-13

## Keywords

containerizing, container, imagen, uso, contenedor, producción, base, fuente, vulnerabilidad, confiable.

## Status

Accepted

Referenced by [ADR CTR 0002. Empleo de imágenes base determinísticas](CTR-0002-empleo-de-imagenes-base-deterministicas.md)

## Context

Empleamos imágenes de contenedores (imágenes base) como punto de partida de nuestro proceso de creación de nuevas imágenes. También, las usamos directamente como soporte funcional de nuestras aplicaciones. Como vemos, independientemente del caso, estas imágenes constituyen un elemento fundamental del proceso de seguridad que permite mitigar sus vulnerabilidades.
 
En la comunidad, existen muchos proveedores de imágenes desde los cuales podemos hacer uso de su contenido. Es fácil encontrar en ellos imágenes disponibles públicamente que concuerden con nuestras necesidades, sin embargo, al igual que ocurre con cualquier entidad de la cual dependemos, debemos ser consientes de cual es su procedencia, ya que no deseamos utilizar imágenes publicadas por proveedores (o usuarios) que no conocemos o que no confiamos.

## Decision

Empleamos imágenes de contenedores de fuentes conocidas y confiables.

Partir de fuentes conocidas nos permite tener algún nivel de garantía de calidad, reducir el número de vulnerabilidades y tener más control sobre lo que se empaqueta dentro de los contenedores.

## Consequences

Requerimos no descargar o instalar imágenes desde proveedores o sitios web que no son de nuestra confianza.

Para ello, requerimos uso de imágenes provenientes de sitios oficiales o el empleo de herramientas (por ejemplo Notary) que permitan publicar y administrar imágenes de contenedores confiables mediante firmas digitales y así, permitir a sus consumidores verificar la integridad y el origen de su contenido.

