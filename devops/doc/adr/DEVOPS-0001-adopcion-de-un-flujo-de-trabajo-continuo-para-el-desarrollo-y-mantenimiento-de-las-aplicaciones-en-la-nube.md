# ADR DEVOPS 0001. Adopción de un flujo de trabajo continuo para el desarrollo y mantenimiento de las aplicaciones en la nube

Date: 2022-12-16

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso.

## Status

Accepted

Referenced by [ADR DEVOPS 0011. Etapas básicas del flujo de trabajo para aplicaciones en la nube basadas en contenedores](DEVOPS-0011-etapas-basicas-del-flujo-de-trabajo-para-aplicaciones-en-la-nube-basadas-en-contenedores.md)

Referenced by [ADR DEVOPS 0005. Uso de infraestructura inmutable para soportar la plataforma de flujo continuo](DEVOPS-0005-uso-de-infraestructura-inmutable-para-soportar-la-plataforma-de-flujo-continuo.md)

Referenced by [ADR MS 0004. Despliegue mediante pipeline](../../../microservice/doc/adr/MS-0004-despliegue-mediante-pipeline.md)

Referenced by [ADR DEVOPS 0007. Uso de imágenes doradas para el despliegue de las aplicaciones en la nube](DEVOPS-0007-uso-de-imagenes-doradas-para-el-despliegue-de-las-aplicaciones-en-la-nube.md)

Referenced by [ADR DEVOPS 0003. Etapas básicas del flujo de trabajo para aplicaciones en la nube basadas en ambientes operativos (maquinas virtuales)](DEVOPS-0003-etapas-basicas-del-flujo-de-trabajo-para-aplicaciones-en-la-nube-basadas-en-ambientes-operativos.md)

Referenced by [ADR DEVOPS 0013. Escaneo de vulnerabilidades en imágenes doradas](DEVOPS-0013-escaneo-de-vulnerabilidades-en-imagenes-doradas.md)

Referenced by [ADR DEVOPS 0019. detección de construcciones sospechosas en archivos Dockerfile](DEVOPS-0019-deteccion-de-construcciones-sospechosas-en-archivos-dockerfile.md)

## Context

La Cloud Native Computing Foundation (CNCF) define a una tecnología en la nube como aquella que permite construir aplicaciones basadas en servicios escalables, bajamente acoplados, resilientes, administrables y observables individualmente; los cuales son capaces de ser ejecutados en ambientes dinámicos públicos, privados o híbridos. Asimismo, junto a esta definición, se establece que estos servicios deben ser acompañados de procesos de automatización robustos que permitan aplicar cambios frecuentes y predecibles a dichos servicios.

## Decision

Implementaremos procesos automáticos y continuos para el desarrollo y el mantenimiento de las aplicaciones en la nube.

La adopción de un flujo continuo y automático implica realizar las siguientes prácticas: Integración Continua y Entrega Continua o Despliegue Continuo.

Con Integración Continua los desarrolladores envían cambios pequeños y frecuentes (varias veces al día) que recorren un flujo en donde se ejecutan pruebas y pasos de compilación automáticos, los cuales están orientados a garantizar que el cambio funcione como se esperaba.  

En el Despliegue Continuo, cada cambio que pasa las etapas del proceso de Integración Continua, se despliega automáticamente a un entorno de preproducción o de producción sin requerir su autorización. Este enfoque no siempre es apropiado, ya que el negocio podría tener consideraciones comerciales que determinen cuando el cambio debería ser liberado.

La Entrega Continua es una práctica en la que cada cambio es una versión lista para la producción. Esta práctica se apoya en la práctica de integración continua, finalizando con la publicación del artefacto de software construido en un repositorio de artefactos. La práctica requiere que un humano decida el momento del despliegue del cambio a un entorno de producción.

## Consequences

La automatización reduce el trabajo manual y mejora la calidad del software, con bucles predecibles y automáticos de retroalimentación de los usuarios que permiten reversiones rápidas y recuperación de fallas. Sin embargo, es importante considerar que presenta varios desafíos:

- La elección del software usado para la implementación del flujo continuo.
  
- Habilidades requeridas en los administradores para configurar y aprovisionar la infraestructura de la plataforma de flujo continuo.
  
- Estrategia usada en el desarrollo y mantenimiento del flujo continuo.
