# ADR DEVOPS 0013. Escaneo de vulnerabilidades en imágenes doradas

Date: 2023-01-06

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, etapas, aprovisionamiento, imagen, infraestructura, inmutable, dorada, vulnerabilidad, escaneo.

## Status

Accepted

References [ADR DEVOPS 0007. Uso de imágenes doradas para el despliegue de las aplicaciones en la nube](DEVOPS-0007-uso-de-imagenes-doradas-para-el-despliegue-de-las-aplicaciones-en-la-nube.md)

References [ADR DEVOPS 0001. Adopción de un flujo de trabajo continuo para el desarrollo y mantenimiento de las aplicaciones en la nube](DEVOPS-0001-adopcion-de-un-flujo-de-trabajo-continuo-para-el-desarrollo-y-mantenimiento-de-las-aplicaciones-en-la-nube.md)

References [ADR DEVOPS 0010. Uso de repositorio de imágenes para almacenamiento de imágenes doradas](DEVOPS-0010-uso-de-repositorio-de-imagenes-para-almacenamiento-de-imagenes-doradas.md)

## Context

Más allá de cumplir con el propósito para el cual fue creada la imagen dorada también, debe garantizase que su configuración sea la adecuada, que el acceso se ha restringido a determinados usuarios y que se empleen mecanismos de seguridad y buenas prácticas que ayuden a descubrir fallos de seguridad en la imagen los cuales, pueden comprometer gravemente el servicio o la organización.

Auditorías rutinarias y búsquedas de vulnerabilidades y exposiciones comunes (CVE) son actividades que ayudan a encontrar fallos de seguridad.  

El análisis de vulnerabilidades de las imágenes permite a los equipos de desarrollo comprobar el estado de seguridad de las imágenes es decir, identificar problemas de seguridad en fuentes, paquetes, bibliotecas y sistema operativo; versiones en las que se introdujeron las fallas y sus posibles soluciones si es que están disponibles.

## Decision

Realizaremos análisis de vulnerabilidades de las imágenes doradas para minimizar el riesgo de fallas de seguridad.

Protegeremos a las aplicaciones nativas en la nube detectando vulnerabilidades, secretos codificados y otros problemas de seguridad durante el ciclo de desarrollo continuo, permitiendo a los desarrolladores solucionar problemas de seguridad rápidamente.

Cada una de las imágenes doradas, almacenadas en repositorios de imágenes, deben ser sometidas a un análisis riguroso basado en listas de vulnerabilidades y exposiciones comunes.

## Consequences

El escaneo de vulnerabilidades es realizado por herramientas automatizadas durante el ciclo de desarrollo continuo, implicando la comprensión y el entendimiento de la herramienta usada como así, el aprovisionamiento de la infraestructura de la plataforma de escaneo de seguridad y su implementación en el ciclo de desarrollo continuo.  

También, como parte de una prueba de penetración en profundidad, puede realizarse manualmente este proceso.
