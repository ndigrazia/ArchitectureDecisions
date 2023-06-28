# ADR FAAS 0026. Despliegue mediante pipeline

## Keywords

faas, serverless, función, sin servidor, servicio, pipeline, despliegue.

## Status

Accepted

Referenced by [ADR FAAS 0022. Definición del limite de concurrencia](FAAS-0022-definicion-del-limite-de-concurrencia.md)

References [ADR FAAS 0025. Desacoplamiento de la tecnología de registro de eventos](FAAS-0025-desacoplamiento-de-la-tecnologia-de-registro-de-eventos.md)

References [ADR DEVOPS 0015. Etapas básicas del flujo de trabajo para aplicaciones en la nube basadas en código sin servidor](../../../devops/doc/adr/DEVOPS-0015-etapas-basicas-del-flujo-de-trabajo-para-aplicaciones-en-la-nube-basadas-en-codigo-sin-servidor.md)

## Context

Integración Continua y Despliegue Continuo son dos practicas fundamentales en el desarrollo y despliegue de aplicaciones basadas en la nube. Estas practicas permiten que el código se refine continuamente mediante pruebas automatizadas y luego, se implemente en el entorno de producción con una mínima intervención manual.

Al igual que los microservicios, las "funciones como un servicio" se implementan de forma independiente. Al automatizar el proceso de su construcción ayudamos a eliminar las tareas manuales del proceso de desarrollo de software y como consecuencia, reducimos la posibilidad de cometer errores y disminuimos los tiempos de entrega de la solución a producción.

## Decision

Desplegamos una "función como un servicio" usando un pipeline de despliegue.

## Consequences

Requerimos el uso de un entorno de ejecución del pipeline de despliegue, la definición de las tareas del pipeline de despliegue y la determinación del momento de ejecución del pipeline de despliegue dentro del proceso de desarrollo de software.
