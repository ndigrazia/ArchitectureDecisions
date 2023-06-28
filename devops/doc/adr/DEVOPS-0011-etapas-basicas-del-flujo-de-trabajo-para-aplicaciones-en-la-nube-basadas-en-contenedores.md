# ADR DEVOPS 0011. Etapas básicas del flujo de trabajo para aplicaciones en la nube basadas en contenedores

## Keywords

devops, microservicio, continuo, entrega, despliegue, flujo, proceso, etapas, automático, contenedor.

## Status

Accepted

References [ADR DEVOPS 0001. Adopción de un flujo de trabajo continuo para el desarrollo y mantenimiento de las aplicaciones en la nube](DEVOPS-0001-adopcion-de-un-flujo-de-trabajo-continuo-para-el-desarrollo-y-mantenimiento-de-las-aplicaciones-en-la-nube.md)

Referenced by [ADR MS 0003. Empaquetado del micro servicio como imagen de contenedor](../../../microservice/doc/adr/MS-0003-empaquetado-del-microservicio-como-imagen-de-contenedor.md)

## Context

La adopción de un flujo de trabajo continuo y automático implica realizar un conjunto de instrucciones o pasos que se ejecutarán cada vez que el equipo de desarrollo registre un cambio o nueva función en el repositorio de código.

Los pasos que componen un flujo de trabajo pueden variar dependiendo del servicio, de la organización y de las estructuras del equipo. Sin embargo, identificar las tareas mínimas en un flujo de trabajo ayudará a garantizar la calidad y la entrega a tiempo del servicio.

## Decision

Implementaremos como mínimo flujos de trabajo para el desarrollo y el mantenimiento de las aplicaciones en la nube basadas en contenedores con las siguientes tareas:

- CheckOut: Extrae los últimos cambios del repositorio de código fuente.

- Enforce Standards: Asegura la calidad de ingeniería identificando desviaciones de un formato estándar (Linting). 
  
- Quality Test: Ejecuta análisis de código estático para medir la calidad del código.

- Binary Build: Instala las dependencias y compila el código, generando un artefacto binario.

- Unit Test: Ejecuta las pruebas unitarias.

- Security Test: Verifica si existen vulnerabilidades conocidas y divulgadas públicamente.

- Image Build: Genera la imagen de contenedor.

- Image Push: Versiona la imagen construida en la etapa anterior y almacena en un repositorio remoto.

- Analyse: Ejecuta el análisis de vulnerabilidades de la imagen.

- Deploy: Despliega la imagen construida desde un repositorio remoto hacia un entorno de prueba/producción.

- Acceptance Test: Ejecuta una serie de pruebas de humo y validación para verificar que la aplicación funciona como se esperaba.

- Roll Back (Si es necesario y si es posible): Ejecuta tareas para desplegar una version previa ante errores encontrados en el despliegue. Considere la alternativa de desplegar una nueva version que solucione el inconveniente (rolling forward).

Los diversos pasos que deben tomarse para mover un trabajo hacia su finalización variarán según el tipo de aplicación o servicio como así también, de los entornos de implementación usados para probar los cambios. Sin embargo, consideramos que las tareas anteriores son fundamentales para mantener un ciclo sano de desarrollo y de mantenimiento de las aplicaciones en la nube basadas en contenedores.

## Consequences

La ejecución de tareas continuas y repetitivas permite construir, empaquetar, probar, validar e implementar con confianza en ambientes pre-producción/producción. Sin embargo, es importante considerar que presenta varios desafíos:

- La elección del software usado para la implementación del flujo continuo.
  
- Habilidades requeridas en los administradores para configurar y aprovisionar la infraestructura de la plataforma de flujo continuo.
  
- Estrategia usada en el desarrollo y mantenimiento del flujo continuo.
