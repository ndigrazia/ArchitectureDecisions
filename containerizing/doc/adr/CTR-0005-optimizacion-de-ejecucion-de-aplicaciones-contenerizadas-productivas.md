# ADR CTR 0005. Optimización de ejecución de aplicaciones contenerizadas productivas

Date: 2023-09-05

## Keywords

containerizing, container, imagen, uso, contenedor, librería, terceros, producción, dependencia, optimización. 

## Status

Accepted

## Context

Rara vez desarrollamos todo el software de nuestras aplicaciones. Generalmente nos apoyamos de funcionalidades ofrecidas por paquetes de terceros mediante bibliotecas y frameworks. Es posible que las funcionalidades brindadas por terceros cuenten con optimizaciones en los diferentes escenarios o ambientes (desarrollo, testing o producción) de ejecución de la aplicación.

## Decision

Aseguramos que los frameworks y bibliotecas que empleamos en la aplicación contenerizada en ambientes productivos utilicen su óptima configuración en rendimiento o en seguridad.

Al ejecutar aplicaciones debemos conocer si las bibliotecas y frameworks que usamos, disponen de optimizaciones y de ser así, cuando y como activarlas para asegurar su optima configuración en rendimiento o en seguridad.

## Consequences

Requerimos identificar si las bibliotecas y frameworks que usamos en nuestra aplicación disponen de optimizaciones para ambientes productivos. En ese caso, requerimos activarlas. 

Por ejemplo, cuando se emplea el framework Node.js, el framework espera que la variable de entorno NODE_ENV tenga el valor de "production" para activar optimizaciones. Algunas de sus librerías, por ejemplo Express, son optimizadas solo en el caso de que dicha variable disponga de ese valor. Como consecuencia, es necesario asignar el valor "production" a la variable NODE_ENV, ya sea cuando se construyen imágenes de contenedores mediante una directiva especifica (por ejemplo, ENV NODE_ENV production) en el archivo que describe los pasos de construcción de la imagen del contenedor (por ejemplo, Dockerfile) o, asignar dicho valor como variable de contexto al momento de ejecutar el contenedor.

El siguiente es un ejemplo que cumple con lo solicitado:

```
FROM node:16.17.0-bullseye-slim
...
# Directiva para la optimización de servicios sobre el Framework Node.js
ENV NODE_ENV production
```

