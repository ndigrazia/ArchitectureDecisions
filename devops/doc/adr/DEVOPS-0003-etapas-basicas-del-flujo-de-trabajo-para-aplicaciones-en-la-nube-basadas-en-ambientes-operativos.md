# ADR DEVOPS 0003. Etapas básicas del flujo de trabajo para aplicaciones en la nube basadas en ambientes operativos (maquinas virtuales)

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, etapas, automático, imágenes, operativas, maquinas virtuales.

## Status

Accepted

References [ADR DEVOPS 0001. Adopción de un flujo de trabajo continuo para el desarrollo y mantenimiento de las aplicaciones en la nube](DEVOPS-0001-adopcion-de-un-flujo-de-trabajo-continuo-para-el-desarrollo-y-mantenimiento-de-las-aplicaciones-en-la-nube.md)

References [ADR DEVOPS 0007. Uso de imágenes doradas para el despliegue de las aplicaciones en la nube](DEVOPS-0007-uso-de-imagenes-doradas-para-el-despliegue-de-las-aplicaciones-en-la-nube.md)

## Context

Las imágenes doradas proporcionan el entorno sobre el cual las aplicaciones se ejecutan. Son fundamentales para garantizar que su aplicación se implemente y escale de manera rápida y confiable. Además, sirven para archivar versiones de aplicaciones para recuperación ante desastres o escenarios de reversión.

Con esta practica, es requerida la adopción de un flujo de trabajo continuo y automático, que permita mediante pasos, generar una nueva imagen cada vez que el equipo de desarrollo registre un cambio o nueva función sobre la misma.

Los pasos que componen un flujo de trabajo pueden variar dependiendo de la organización y de las estructuras del equipo. Sin embargo, identificar las tareas mínimas en un flujo de trabajo ayudará a garantizar la calidad y la entrega a tiempo del servicio.

## Decision

Implementaremos como mínimo flujos de trabajo para el desarrollo y el mantenimiento de imágenes de ambientes operativas con las siguientes tareas:

- Depart: Crea una instancia a partir de una imagen dorada base sanitizada.
  
- Supply: Personaliza o aprovisiona la imagen de partida según las necesidades buscadas.

- Push: Publicar la imagen personalizada en un repositorio de imágenes.

- Analyse: Ejecuta el análisis de vulnerabilidades de la imagen.

- Deploy: Despliega la imagen construida desde un repositorio remoto hacia un entorno de prueba/producción.

- Acceptance Test: Ejecuta una serie de pruebas de humo y validación para verificar que la imagen funciona como se esperaba.

- Roll Back (Si es necesario y si es posible): Ejecuta tareas para desplegar una version previa ante errores encontrados en el despliegue. Considere la alternativa de desplegar una nueva version que solucione el inconveniente (rolling forward).

Las imágenes de ambientes operativos también son conocidas como imágenes de máquinas virtuales (VM).

Los diversos pasos que deben tomarse para generar una imagen de ambiente operativa variarán según el tipo de aplicación y entornos de implementación usados para probar los cambios. Sin embargo, consideramos que las tareas anteriores son fundamentales para mantener un ciclo sano de desarrollo y de mantenimiento de imágenes de ambientes operativos.

Finalmente, el proceso de  creación de imágenes debe ser reproducible, auditable, configurable, confiable, automático y repetible.

## Consequences

La ejecución de tareas continuas y repetitivas permite construir, empaquetar, probar, validar e implementar con confianza las imágenes en ambientes pre-producción/producción. Sin embargo, es importante considerar que presenta varios desafíos:

- La elección del software usado para la implementación del flujo continuo.
  
- Habilidades requeridas en los administradores para configurar y aprovisionar la infraestructura de la plataforma de flujo continuo.
  
- Estrategia usada en el desarrollo y mantenimiento del flujo continuo.
