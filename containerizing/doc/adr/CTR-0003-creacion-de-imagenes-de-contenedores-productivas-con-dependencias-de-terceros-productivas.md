# ADR CTR 0003. Creación de imágenes de contenedores productivas con dependencias de terceros productivas

Date: 2023-08-30

## Keywords

containerizing, container, imagen, uso, contenedor, librería, terceros, producción, dependencia. 

## Status

Accepted

Referenced by [ADR CTR 0005. Optimización de ejecución de aplicaciones contenerizadas productivas](CTR-0005-optimizacion-de-ejecucion-de-aplicaciones-contenerizadas-productivas.md)

Referenced by [ADR CTR 0011. Prevención de fuga de información confidencial durante la descarga de librerías de terceros](CTR-0011-prevencion-de-fuga-de-informacion-confidencial-durante-la-descarga-de-librerias-de-terceros.md)

## Context

Durante la construcción de la imagen de contenedor incluimos herramientas o librerías de terceros como medio de soporte de las funcionalidades del servicio ofrecido por el contenedor. Al instalar estos componentes de terceros podemos incluir ciertas dependencias que no son requeridas para su funcionamiento en producción como por ejemplo, librerías usadas durante su desarrollo o en las fases de pruebas. 

El agregado de dependencias no requeridas para la ejecución del contenedor en producción, provoca el incremento del tamaño de la imagen del contenedor y aumenta el riesgo de poseer más vulnerabilidades.

## Decision

Incluimos solamente dependencias de terceros productivas en imágenes de contenedores productivas.

Aseguramos construcciones determinísticas para garantizar que no hay desviaciones durante el proceso de construcción automático (CI/CD) que provoquen la inclusión de dependencias no requeridas.

La adecuada inclusión de las dependencias permite reducir el tamaño de la imagen del contenedor y por consiguiente, reducir el riesgo de vulnerabilidades, el tiempo de descarga y el espacio de almacenamiento.

## Consequences

Requerimos construcciones determinísticas, estableciendo claramente las dependencias a ser incluidas durante cada fase del proceso de construcción de la imagen del contenedor. Para ello empleamos los mecanismos ofrecidos por las herramientas o por el propio lenguaje de construcción del contenedor. Por ejemplo, empleamos la instrucción "npm ci --only=production" para la inclusión de dependencias productiva en imágenes de contenedores basados en el framework node.js y en el gestor de paquetes npm.

El siguiente es un ejemplo que cumple con lo solicitado:

```
FROM node:16.17.0-bullseye-slim
..
# La mejor práctica para la instalación de dependencias productivas
# bajo el Framework Node.js
RUN npm ci --only=production
...
```

