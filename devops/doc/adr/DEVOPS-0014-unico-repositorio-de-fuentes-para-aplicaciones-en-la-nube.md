# ADR DEVOPS 0014. Único repositorio de fuentes para aplicaciones en la nube

## Keywords

devops, repositorio, fuente, contenedor, código, aplicación, nube.

## Status

Accepted

Supercedes [ADR MS 0005. Único repositorio de fuentes](../../../microservice/doc/adr/MS-0005-unico-repositorio-de-fuentes.md)

## Context

En ingeniería de software es sumamente importante identificar y controlar los activos que se producen como resultado del proceso de desarrollo de software. Los fuentes forman uno de esos activos, los cuales necesitan control de sus cambios. Los sistemas de control de versiones ayudan en esa tarea permitiendo trazar los cambios y observar cada modificación realizada sobre los fuentes. Con el objetivo de poder cumplir con su propósito, los fuentes perteneciente al aplicativo, se almacenan siempre en un único repositorio, el cual está gestionado por un sistemas de control de versiones. Asimismo, aunque es posible contar con un conjunto de repositorios como es el caso de sistemas de controles de versiones descentralizado (Git), siempre se garantiza la correlación entre el código fuente perteneciente al aplicativo.

## Decision

Almacenamos el código fuente de las aplicaciones en la nube en un único repositorio de código fuente.

Siempre hay una correlación uno a uno entre el código base y la versión de la aplicación en la nube, lo que facilita la traza de los cambios y la funcionalidad asociada.

El código fuente es el mismo para una misma version, aunque pueden estar activas diferentes versiones en cada implementación de la aplicación en la nube.

## Consequences

Requerimos el uso de un sistema de control de versiones, vincular el código fuente de la aplicación en la nube a un solo repositorio, independiente de la cantidad de imágenes construidas o instancias ejecutadas en diferentes ambientes o dominios.
