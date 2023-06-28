# ADR DEVOPS 0015. Etapas básicas del flujo de trabajo para aplicaciones en la nube basadas en código sin servidor

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, etapas, automático, código, sin servidor, serverless.

## Status

Accepted

Referenced by [ADR FAAS 0026. Despliegue mediante pipeline](../../../function-as-a-service/doc/adr/FAAS-0026-despliegue-mediante-pipeline.md)

## Context

Las aplicaciones en la nube basadas en código sin servidor (serverless) han tenido un rápido crecimiento debido al hecho de permitir desarrollar aplicaciones que entregan la total responsabilidad de la infraestructura al proveedor de la nube. Es decir, el equipo de desarrollo solamente suministra el código de la aplicación, delegando al proveedor de la nube el aprovisionamiento de su contexto de ejecución.

La arquitectura basadas en código sin servidor presenta varios desafíos, uno de los cuales es el flujo continuo de desarrollo y de despliegue.

## Decision

Implementaremos como mínimo flujos de trabajo para el desarrollo y el mantenimiento de las aplicaciones en la nube basadas en código sin servidor con las siguientes tareas:

- CheckOut: Extrae los últimos cambios del repositorio de código fuente.

- Enforce Standards: Asegura la calidad de ingeniería identificando desviaciones de un formato estándar (Linting). 
  
- Quality Test: Ejecuta análisis de código estático para medir la calidad del código.

- Build: Instala las dependencias y compila el código (en caso de requerirlo), generando un artefacto binario.

- Unit Test: Ejecuta las pruebas unitarias.

- Security Test: Verifica si existen vulnerabilidades conocidas y divulgadas públicamente.

- Package: Genera el paquete que contiene el entregable de la aplicación con su correspondiente numero de versión.

- Push: Almacena el paquete resultante en un repositorio remoto.

- Deploy: Desde el repositorio remoto actualiza y publica la aplicación en el contexto de ejecución del proveedor de la nube.

- Acceptance Test: Ejecuta una serie de pruebas de humo y validación para verificar que la aplicación funciona como se esperaba.

- Roll Back (Si es necesario y si es posible): Ejecuta tareas para desplegar una version previa ante errores encontrados en el despliegue. Considere la alternativa de desplegar una nueva version que solucione el inconveniente (rolling forward).

Los diversos pasos que deben tomarse para generar el entregable pueden variar, sin embargo, consideramos que las tareas anteriores son fundamentales para mantener un ciclo sano de desarrollo y de mantenimiento de aplicaciones basadas en código sin servidor.

## Consequences

La ejecución de tareas continuas y repetitivas permite construir, empaquetar, probar, validar e implementar con confianza en ambientes pre-producción/producción. Sin embargo, es importante considerar que presenta varios desafíos:

- La elección del software usado para la implementación del flujo continuo.
  
- Habilidades requeridas en los administradores para configurar y aprovisionar la infraestructura de la plataforma de flujo continuo.
  
- Destreza en la implementación del flujo continuo de trabajo.

- Habilidades requeridas en los administradores para configurar y mantener los recursos de la infraestructura del proveedor de la nube sobre la cual se desplegarán las aplicaciones de código sin servidor.
