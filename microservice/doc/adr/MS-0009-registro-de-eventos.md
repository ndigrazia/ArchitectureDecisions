# ADR MS 0009. Registro de eventos

Date: 2022-08-18

## Keywords

microservicio, evento, log, mensaje, registro, soporte.

## Status

Accepted

References [ADR MS 0006. Configuración elástica](MS-0006-configuracion-elastica.md)

## Context

El registro de mensajes con información de lo que sucede dentro de una aplicación o servicio es comúnmente conocido como log, y es de gran utilidad para los administradores/desarrolladores y en especial para el equipo de soporte. 

Los mensajes con información ahorran muchas horas valiosas tanto para el equipo de soporte como para los desarrolladores en el diagnostico como en la resolución de problemas.

## Decision

Usamos mecanismos para registrar o mostrar mensajes con información de lo que está sucediendo en el microservicio, con el fin de facilitar el diagnóstico de problemas y reducir el tiempo de su resolución.

Dado que los microservicios se pueden implementar con diversos lenguajes de programación, existen librerías o mecanismos convenientes en cada uno de esos lenguajes que nos pueden ayudar con la tarea de registro de eventos.

## Consequences

Requerimos el uso de librerías o de bibliotecas externas para implementar el registro de mensajes, publicación de mensajes en la salida estándar (stdout) con diferentes niveles de severidad (errors, warnings, information and debug) y configuración de la estrategia de registro de mensajes, sin necesidad de cambiar el código o construir nuevamente la imagen del microservicio (Configuración elástica).

Finalmente, es importante disponer de una solución que implemente el patrón Log Aggregation para centralizar el servicio de registro de mensajes, permitiendo buscar y analizar los mensajes como así también, configurar alertas que se disparan cuando aparecen ciertos mensajes en los registros.
