# ADR MSG 0003. Eliminación de mensajes basura encolados

Date: 2022-08-23

## Keywords

messaging, message, asincrónica, idempotente, mensaje, cola, basura, eliminación.

## Status

Accepted

Referenced by [ADR MSG 0005. Definición del tamaño de la cola de mensajería](MSG-0005-definicion-del-tamano-de-la-cola-de-mensajeria.md)

References [ADR MSG 0006. Creación de un procesador de mensajes basura encolados](MSG-0006-creacion-de-un-procesador-de-mensajes-basura-encolados.md)

## Context

Puede ocurrir que algunos de los mensajes almacenados en la cola de mensajes no se procesen correctamente debido al contenido del propio mensaje, haciendo que el mensaje retorne a la cola para otro intento de procesamiento (client acknowledge mode).

Cuando un mensaje permanece en la cola durante mucho tiempo debido a que no puede ser procesado adecuadamente, se transforma en un mensaje basura, provocando reiterados procesamientos que terminan afectando el rendimiento de la solución.

## Decision

Detectamos y eliminamos mensajes basura dentro de la cola de mensajes asincrónicos, enviandolos a otra cola que contenga los mensajes no tratados. 

Comúnmente, es llamada dead-letter a la cola que cumple el rol de almacenar mensajes no tratados.

El consumidor o el propio sistema de mensajería (broker) es el responsable de enviar los mensajes no tratados a la cola dead-letter.

La eliminación de mensajes basura ayuda a garantizar la disponibilidad y el rendimiento de la solución.

## Consequences

Requerimos usar una variable de conteo que permite conocer la cantidad de veces que se intentó procesar al mensaje, almacenar el mensaje basura detectado en otro medio (dead-letter) para luego, poder ser tratado, ya sea manual o automáticamente. Y finalmente, establecer, de acuerdo a las definiciones del negocio, como realizar el tratamiento de los mensajes basura.
