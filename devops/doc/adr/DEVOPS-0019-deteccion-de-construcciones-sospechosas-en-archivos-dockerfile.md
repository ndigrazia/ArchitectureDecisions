# ADR DEVOPS 0019. Detección de construcciones sospechosas en archivos Dockerfile

Date: 2023-02-15

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, etapas, imagen, automático, infraestructura, inmutable, dorada, imágenes.

## Status

Accepted

References [ADR DEVOPS 0007. Uso de imágenes doradas para el despliegue de las aplicaciones en la nube](DEVOPS-0007-uso-de-imagenes-doradas-para-el-despliegue-de-las-aplicaciones-en-la-nube.md)

References [ADR DEVOPS 0001. Adopción de un flujo de trabajo continuo para el desarrollo y mantenimiento de las aplicaciones en la nube](DEVOPS-0001-adopcion-de-un-flujo-de-trabajo-continuo-para-el-desarrollo-y-mantenimiento-de-las-aplicaciones-en-la-nube.md)

## Context

La generación de imágenes doradas para aplicaciones basadas en contenedores es una etapa fundamental del flujo de trabajo continuo. Durante el proceso de construcción de la imagen de contenedor se van leyendo las instrucciones desde un documento de texto (Dockerfile) que contiene todos los comandos, ordenados, para ensamblar una nueva imagen.

El uso inadecuado de las instrucciones usadas durante el proceso de construcción de las imágenes doradas de contenedor puede ocasionar que los contenedores sean lentos al momento de su lanzamiento, con altos costos de almacenamiento y más inseguros.

Los problemas de generados por imágenes mal construidas pueden provocar perdidas cuantiosas para el negocio.

## Decision

Usaremos una solución que ayude a crear imágenes de contenedor siguiendo las mejores prácticas.

La solución tendrá la responsabilidad de analizar los comandos, que componen el archivo que se empleará para generar la imagen de contenedor, basado en las mejores prácticas.

El proceso de construcción deberá ser cancelado en caso de no cumplir con las mejores prácticas, motivando que la nueva imagen no sea generada.

## Consequences

La construcción de imágenes de contenedor siguiendo las mejores prácticas permite crear imágenes pequeñas, seguras, eficientes y fáciles de mantener. Sin embargo, es importante considerar que presenta varios desafíos:

- Determinar donde se ubicará el proceso dentro del flujo continuo de generación de la imagen.

- Empleo y entendimiento de la herramienta para el chequeo del documento Dockerfile.

- Establecimiento de las mejores prácticas y métodos recomendados para construir imágenes eficientes.
