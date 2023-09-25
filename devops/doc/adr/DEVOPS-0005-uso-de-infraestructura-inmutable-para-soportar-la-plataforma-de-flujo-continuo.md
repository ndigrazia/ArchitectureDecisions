# ADR DEVOPS 0005. Uso de infraestructura inmutable para soportar la plataforma de flujo continuo

Date: 2022-12-26

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, etapas, automático, infraestructura, imagen, inmutable.

## Status

Accepted

References [ADR DEVOPS 0001. Adopción de un flujo de trabajo continuo para el desarrollo y mantenimiento de las aplicaciones en la nube](DEVOPS-0001-adopcion-de-un-flujo-de-trabajo-continuo-para-el-desarrollo-y-mantenimiento-de-las-aplicaciones-en-la-nube.md)

References [ADR DEVOPS 0007. Uso de imágenes doradas para el despliegue de las aplicaciones en la nube](DEVOPS-0007-uso-de-imagenes-doradas-para-el-despliegue-de-las-aplicaciones-en-la-nube.md)

## Context

Aprovisionar y mantener actualizado el software de flujo continuo es una práctica crucial. Necesitamos implementar el software de base y luego, desplegar y configurar el software de flujo continuo (software de propósito). Finalmente, debemos mantenerlo actualizado para su estabilidad, su seguridad y sus nuevas funcionalidades.

Las prácticas del pasado requerían de actividades manuales durante el aprovisionamiento del software de base como del software de propósito, asiendo que el proceso sea poco eficiente, largo, doloroso y propenso a errores.

Nuevas prácticas como la infraestructura inmutable permiten la creación de componentes inmutables que se crean, empaquetan los cambios (actualizaciones) y reemplazan el software existente en lugar de actualizarlo.

## Decision

Empaquetaremos y configuramos el software de flujo continuo en un archivo de imagen (imagen dorada).

Realizaremos la implementación y el aprovisionamiento del software de flujo continuo en función de la nueva imagen, destruyendo la anterior implementación. Este proceso se conoce como infraestructura inmutable.

## Consequences

Implementar el software de plataforma continua como infraestructura inmutable ayuda a:

- Reducir los errores, disminuir las inconsistencias y mejorar la confiabilidad en el proceso de aprovisionamiento.

- Eliminar el tiempo de inactividad durante el reemplazo de la instancia, ya que se tienen múltiples instancias en servicio en un momento dado.

- Retornar rápidamente a un estado "perfecto" si las cosas salen mal.

El empleo de esta práctica requiere considerar ciertos aspectos:

- Especificar y mantener el proceso de construcción y de despliegue de las imágenes.

- Definir la estrategia usada en el control de cambios de las imágenes.

- Empleo y entendimiento de una herramienta de aprovisionamiento de infraestructura.

- Empleo y entendimiento de una herramienta de almacenamiento de imágenes (repositorio de imágenes).
