# ADR DEVOPS 0009. Versionado semántico de las imágenes doradas

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, etapas, versionado, semántico, aprovisionamiento, imagen, infraestructura, inmutable, dorada.

## Status

Accepted

References [ADR DEVOPS 0010. Uso de repositorio de imágenes para almacenamiento de imágenes doradas](DEVOPS-0010-uso-de-repositorio-de-imagenes-para-almacenamiento-de-imagenes-doradas.md)

## Context

El uso de imágenes como medio de entrega han simplificado la forma en que desarrollamos y desplegamos las aplicaciones. Sin embargo, esta practica requiere de mecanismos de control de versiones para indicar los cambios realizados durante el ciclo de vida de una imagen, permitiendo rastrear las modificaciones hechas en un momento particular.

Como consecuencia del control de cambios, debemos determinar qué tipo de estrategia usar para el etiquetado de imágenes.

## Decision

Usaremos el versionado semántico para el versionado de las imágenes doradas.

Existen diversas estrategias para el versionado de las imágenes:

- Digest: Cada imagen tiene una identificación única. Un código hash utilizando el algoritmo SHA265.

- Image Tag: La etiqueta es una referencia que indica la arquitectura soportada, el ambiente al cual es aplicable, la aplicación o servicio contenido.

- Semántico: La imagen es nombrada de acuerdo a tres partes: cambios incompatibles,cambios compatibles y parches.

- Timestamp: Se asocia a la imagen el momento en el cual fue generada.

- Build ID: Identificación única de la aplicación o servicio contenido en la imagen. Es similar a la estrategia de Digest.

La estrategia de versionado semántico es sumamente adecuada para el etiquetado de las imágenes, ya que asociar el conjunto de cambios (changesets) realizados en la imagen y así, comprender la funcionalidad utilizada en un momento dado.

Las estrategias de Timestamp, Build ID o Digest dificultan la comprensión de los cambios realizados a la imagen en su ciclo de vida, haciendo difícil para el usuario comprender la funcionalidad utilizada en un momento dado.

Finalmente, dado que una imagen puede cambiar su tag a lo largo de su ciclo de vida, ya que los mismos son mutables, se dificulta conocer si la imagen que se está utilizando es la que realmente se quiere utilizar. Ejemplo de esto, es el uso de la etiqueta "latest" que en un momento determinado referencia a una versión concreta de la imagen, la cual puede ser diferente con el paso del tiempo.

## Consequences

Un mal entendimiento del esquema de versionado semántico no permitirá señalar adecuadamente los cambios y como consecuencia, cambios importantes pueden no ser liberados o llevar a una liberación de cambios en un momento inadecuado. Esto último es bastante fácil de mitigar con el aprendizaje y la utilización de herramientas de automatización.
