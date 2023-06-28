# ADR MS 0006. Configuración elástica

## Keywords

microservicio, configuración, despliegue, elástica.

## Status

Accepted

References [ADR MS 0002. Plataforma centrada en contenedores](MS-0002-plataforma-centrada-en-contenedores.md)

Referenced by [ADR MS 0009. Registro de eventos](MS-0009-registro-de-eventos.md)

## Context

Cuando desarrollamos una aplicación es una buena práctica externalizar los aspectos de su configuración para que podamos cambiar su comportamiento en tiempo de ejecución sin la necesidad de cambiar su código, compilar y empaquetar nuevamente. 

La información de configuración en el ambiente productivo generalmente se desconoce en el momento del desarrollo, solo en tiempo de ejecución podemos aplicar la información correcta para configurar nuestra aplicación.

## Decision

Modificamos los datos de configuración sin necesidad de construir o de empaquetar nuevamente el microservicio en una nueva imagen de contenedor.

Para abordar la necesidad de aplicar y modificar dinámicamente las configuraciones en una implementación del microservicio, se necesita un mecanismo estándar capaz de permitir modificar su comportamiento sin necesidad de ser desarrollado y empaquetado nuevamente.

Dado que los microservicios se pueden implementar con diversos lenguajes de programación, existen librerías o mecanismos convenientes en cada uno de esos lenguajes que nos pueden ayudar con la tarea de configuración.

## Consequences

Requerimos el uso de frameworks o de librerías y la definición de estrategias que permitan implementar dinámicamente configuraciones externalizadas.
