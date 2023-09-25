# ADR FAAS 0020. Estrangulador

Date: 2023-03-20

## Keywords

faas, serverless, función, sin servidor, servicio, estrangulador, strangle, patrón.

## Status

Accepted

Referenced by [ADR FAAS 0001. Monolítica](FAAS-0001-monolitica.md)

## Context

Con la evolución de la tecnológica muchas aplicaciones creadas a partir de ella comienzan a quedar obsoletas. Llevar adelante el reemplazo de un una aplicación por completo puede ser una enorme tarea sujeta a muchas complicaciones. A menudo, una migración gradual es una mejor alternativa. Al mantener los servicios anteriores, para manejar funciones que aún no se han migrado, se logra una transición mas armonica. Sin embargo, esto presenta el inconveniente de tener dos versiones separadas de una misma aplicación, una con las funcionalidades migradas y la otra con las funciones aun no sustituidas. Como resultado, los clientes deben saber dónde se encuentran las funciones particulares, haciendo que deban adecuarse a la nueva ubicación cada vez que se migre un servicio.

Para evitar el impacto generado por los cambios incrementales sobre los clientes podemos crear un componente cuya tarea es interceptar y dirigir las solicitudes a la aplicación heredada o a los nuevos servicios.

## Decision

Implementaremos o diseñaremos una "función como un servicio" como medio para sustituir una aplicación heredada en forma gradual en aquellos servicios con cargas impredecibles y cuyo uso no es muy frecuente.

Implementaremos "funciones como servicio" que mapeen a una sola tarea bien definida.

Descompondremos toda la lógica en servicios individuales, mapeando una "función como un servicio" a una sola tarea bien definida.

Las funciones resultantes se publican en rutas de API Gateway.

El API Gateway (Strangler Facade) distribuye las solicitudes a la aplicación heredada o al nuevo servicio desarrollado con una "función como un servicio".

El objetivo de construir una "función como un servicio" es segregar la lógica de negocio de una manera tal que pueda ser asociada a una función independiente y altamente desacoplada.

## Consequences

Asociaremos cada función con una ruta de API Gateway enfrente de esta.

Los beneficios de ejecutar una función con una responsabilidad claramente definida son:

- Tamaño de paquete más reducido, el cual es determinate en el tiempo de inicio de la "función como un servicio".

- Facilidad en el otorgamiento de privilegios de accesos.

- Facilidad de actualización a nivel de la función sin afectar toda la carga de trabajo.

- Sencillez de prueba.

- Simple de mantener, ya que es más fácil cuando se trabaja con un solo servicio pequeño que con uno monolítico.

- Escalamiento independiente.

Requerimos una plataforma de ejecución de la solución sin servidor.

Requerimos una solución de API Gateway que dirija el trafico.

Finalmente, asociar una única responsabilidad por función presenta complejidad en el diseño y en el mantenimiento a medida que el número de funciones aumenten. También, requiere esfuerzo en la descomposición.
