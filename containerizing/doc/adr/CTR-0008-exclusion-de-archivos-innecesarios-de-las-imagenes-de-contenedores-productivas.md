# ADR CTR 0008. Exclusión de archivos innecesarios de las imágenes de contenedores productivas

Date: 2023-09-11

## Keywords

containerizing, container, imagen, uso, contenedor, producción, sistema operativo, optimización.

## Status

Accepted

## Context

En el transcurso del proceso de construcción de la imagen de contenedor, tenemos la posibilidad de añadir en su interior archivos o directorios almacenados de forma local. Durante la copia del contenido podemos incluir recursos locales no deseados como claves, librerías, archivos de configuración, archivos de depuración, etc.

El agregado de archivos o directorios no deseados provoca el incremento del tamaño de la imagen del contenedor y aumenta el riesgo de poseer más vulnerabilidades.

## Decision

Incluimos un archivo de configuración que describe los archivos y directorios que se desea excluir de la imagen de contenedor.

Al especificar archivos que no se incluirán en la imagen se puede reducir su tamaño y evitar futuros inconvenientes de seguridad causado por perdida de información sensible.

## Consequences

Requerimos disponer de un archivo de configuración que describa los archivos y directorios que se desea excluir de la imagen de contenedor.

Requerimos describir mediante el uso de wildcards, patrones y excepciones los recursos a omitir.

El siguiente es un ejemplo usando el archivo .dockerignore que cumple con lo solicitado:

```
.dockerignore
node_modules
npm-debug.log
Dockerfile
.git
.gitignore
.npmrc
```

