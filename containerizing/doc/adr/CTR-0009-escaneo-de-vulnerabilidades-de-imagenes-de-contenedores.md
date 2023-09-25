# ADR CTR 0009. Escaneo de vulnerabilidades de imágenes de contenedores

## Keywords

containerizing, container, imagen, uso, contenedor, producción, escaneo, vulnerabilidad.

## Status

Accepted

## Context

Las imágenes de contenedores, al igual que cualquier pieza de software, son potenciales fuentes de vulnerabilidades. La detección temprana de sus vulnerabilidades, previa a su instanciación mediante contenedores, evita que sus amenazas se activen y provoquen riesgos de seguridad en el sistema.

## Decision

Escaneamos e identificamos vulnerabilidades dentro de las imágenes de contenedores.

Las vulnerabilidades en una imagen de contenedor se pueden introducir de varias maneras: dependencia de otras imágenes, instalación de herramientas, dependencias de librerías de terceros, configuraciones de red y almacenamiento, etc. El escaneo de vulnerabilidades analiza los componentes que constituyen a la imagen del contenedor para detectar amenazas de seguridad.

## Consequences

Requerimos el uso de una herramienta o escáner de vulnerabilidades de contenedores.

Requerimos el análisis frecuente de vulnerabilidades de imágenes de contenedor almacenadas en los registros de imágenes (images registry). 

Requerimos integrar el escaneo de vulnerabilidades de contenedores en el flujo de integración continua y entrega continua (CI/CD).

