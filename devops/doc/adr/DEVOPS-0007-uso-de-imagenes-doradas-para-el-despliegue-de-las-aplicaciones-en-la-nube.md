# ADR DEVOPS 0007. Uso de imágenes doradas para el despliegue de las aplicaciones en la nube

Date: 2022-12-26

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, etapas, imagen, automático, infraestructura, inmutable, dorada, imágenes.

## Status

Accepted

Referenced by [ADR DEVOPS 0005. Uso de infraestructura inmutable para soportar la plataforma de flujo continuo](DEVOPS-0005-uso-de-infraestructura-inmutable-para-soportar-la-plataforma-de-flujo-continuo.md)

References [ADR DEVOPS 0001. Adopción de un flujo de trabajo continuo para el desarrollo y mantenimiento de las aplicaciones en la nube](DEVOPS-0001-adopcion-de-un-flujo-de-trabajo-continuo-para-el-desarrollo-y-mantenimiento-de-las-aplicaciones-en-la-nube.md)

Referenced by [ADR DEVOPS 0003. Etapas básicas del flujo de trabajo para aplicaciones en la nube basadas en ambientes operativos (maquinas virtuales)](DEVOPS-0003-etapas-basicas-del-flujo-de-trabajo-para-aplicaciones-en-la-nube-basadas-en-ambientes-operativos.md)

Referenced by [ADR MS 0003. Empaquetado del micro servicio como imagen de contenedor](../../../microservice/doc/adr/MS-0003-empaquetado-del-microservicio-como-imagen-de-contenedor.md)

Referenced by [ADR DEVOPS 0008. Escalamiento automático de la plataforma de flujo continuo](DEVOPS-0008-escalamiento-automatico-de-la-plataforma-de-flujo-continuo.md)

Referenced by [ADR DEVOPS 0013. Escaneo de vulnerabilidades en imágenes doradas](DEVOPS-0013-escaneo-de-vulnerabilidades-en-imagenes-doradas.md)

Referenced by [ADR DEVOPS 0019. detección de construcciones sospechosas en archivos Dockerfile](DEVOPS-0019-deteccion-de-construcciones-sospechosas-en-archivos-dockerfile.md)

## Context

Tradicionalmente cuando se deseaba desplegar una aplicación en un ambiente (desarrollo, preproducción o producción) se realizaba el pedido, mediante formularios o aplicaciones web, con la guía de instalación, la cual era empleada por el equipo de operaciones para el armado de la infraestructura, instalación y configuración tanto del software de base como el software de propósito. Las actividades de aprovisionamiento de la aplicación eran realizadas manualmente, asiendo que los procedimientos empleados sean susceptibles de errores, imposibles de evaluar e incapaces de repetir.

El empleo de las prácticas pasadas limitan los beneficios que una organización puede obtener sobre las tecnologías en la nube: escalado automático, reparación automática, alta disponibilidad o tolerancia a fallas.

Las imágenes doradas (golden image), como alternativa a los procesos manuales, permiten que el aprovisionamiento y la configuración del software de base más el software de propósito, es decir el estado deseado, se realice una única vez y luego se reuse en diferentes entornos de la organización.

## Decision

Usaremos imágenes doradas para empaquetar, transportar y desplegar las aplicaciones en la nube.

Nos referimos a imágenes doradas como aquellas que incluyen los componentes de software (sistema operativo, código de aplicación, bibliotecas, herramientas, dependencias y otros archivos) necesarios para ejecutar la aplicación. También se las conoce como imágenes maestras, imágenes base o imágenes plantillas. Su fundamental característica es que son inmutables y son usadas para crear ambientes de ejecución.

Las imágenes doradas son una abstracción de las imágenes de ambientes operativos (máquinas virtuales) y de las imágenes de contenedores.

Tanto las imágenes de ambientes operativos como las imágenes de contenedor definen un contexto basado en software (en lugar de uno físico) para ejecutar programas e implementar aplicaciones. Sus diferencias radican en su arquitectura de solución y en el tamaño de las mismas.

Las imágenes doradas almacenan el aprovisionamiento y la configuración del software de base más el software de propósito, garantizando la ejecución de la aplicación en forma aislada, sin necesidad de ninguna modificación de la misma luego de su construcción.

Las imágenes construidas son almacenadas en repositorios desde donde, se reúsan en diversas partes de la organización.

Cualquier proceso de modificación de la imagen dorada requiere la generación de una nueva versión de la imagen dorada. El proceso de generación de una nueva imagen implica tener un flujo de trabajo de integración continua y de entrega continua.

## Consequences

El uso de imágenes doradas permite reducir el numero de errores que el equipo de operaciones puede cometer, porque automatiza las tareas de aprovisionamiento en flujos de trabajo. Asimismo, ahorra tiempo de despliegue, ya que cada imagen es aislada y contiene todo lo necesario para su ejecución. Finalmente, asegura consistencia porque el estado deseado de la aplicación se mantiene consistente a lo largo de los entornos de ejecución.

El uso de imágenes doradas requiere:

- Determinar la estrategia usada en el flujo continuo para la generación de la imagen.

- Definición de la estrategia usada en el control de cambios en las imágenes.

- Empleo y entendimiento de una herramienta de almacenamiento de imágenes (repositorio de imágenes).

- Empleo y entendimiento del software usado para la implementación del flujo continuo.
