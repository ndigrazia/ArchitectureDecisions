# ADR FAAS 0025. Desacoplamiento de la tecnología de registro de eventos

Date: 2023-03-22

## Keywords

faas, serverless, función, sin servidor, servicio, evento, log, mensaje, registro, soporte.

## Status

Accepted

Referenced by [ADR FAAS 0026. Despliegue mediante pipeline](FAAS-0026-despliegue-mediante-pipeline.md)

## Context

Durante una falla, el registro de mensajes dentro de un servicio le permite detallar información importante que puede ser necesaria para comprender lo ocurrido. Anexar información durante la ejecución de un código ayuda a entender como es el funcionamiento del sistema en el mundo real.

La capacidad de escalamiento de una función puede causar problemas con otros servicios que no escalan de la misma manera. Es posible que el sistema de registro de mensajes (logging system) propio de una organización no pueda manejar los picos de escalamiento de las funciones, ya que las mismas pueden escalar a grandes magnitudes al instante y contraerse (hasta cero) sin que el sistema que recibe sus registros pueda actuar en consecuencia.

## Decision

Utilizaremos los mecanismos ofrecidos por la plataforma en la nube para el registro de eventos de una "función como un servicio".

En caso de contar con un sistema de registro propio, desacoplaremos las funciones usando una arquitectura asincrónica basada en colas o eventos para la ingesta de los datos del sistema de registro del proveedor de la nube a su propio sistema.

## Consequences

Requerimos una plataforma de ejecución de la solución sin servidor.

Requerimos el uso una tecnológica asincrónica para la ingesta de los registros en los sistemas propios. 

Requerimos conocer y entender los mecanismos ofrecidos por el proveedor en la nube para el manejo de registros.

Desacoplando el sistema de registro de eventos de las peticiones de los usuarios permitimos que se pueda realizar la escritura de los eventos y las búsquedas de datos en el sistema de registro cuando ocurra un aumento de la carga.
