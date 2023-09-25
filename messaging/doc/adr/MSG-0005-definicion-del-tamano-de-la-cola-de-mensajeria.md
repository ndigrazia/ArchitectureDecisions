# ADR MSG 0005. Definición del tamaño de la cola de mensajería

Date: 2022-08-24

## Keywords

messaging, message, asincrónica, mensaje, cola, tamaño.

## Status

Accepted

References [ADR MSG 0003. Eliminación de mensajes basura encolados](MSG-0003-eliminacion-de-mensajes-basura-encolados.md)

Referenced by [ADR MSG 0006. Creación de un procesador de mensajes basura encolados](MSG-0006-creacion-de-un-procesador-de-mensajes-basura-encolados.md)

## Context

Controlar el tamaño de las colas, evitando que crezcan indefinidamente, ayuda a mejorar el rendimiento del sistema de mensajería (broker), evita que un crecimiento de los mensajes terminen en un agotamiento de los recursos de memoria, impide el incremento en el tiempo de procesamiento de los mensajes y previene que las transacciones para resolver la solicitud queden bloqueadas esperando la disponibilidad del recurso del sistema de mensajería.

## Decision

Establecemos la longitud máxima de mensajes que una cola de mensajería puede almacenar.

La definición del tamaño de la cola de mensajería puede realizarse en función del número determinado de mensajes o a un número determinado de bytes.

## Consequences

Requerimos limitar la longitud máxima de una cola a un número determinado de mensajes o a un número determinado de bytes y, establecer el comportamiento a realizar cuando la cola alcance su tamaño máximo: Descartar mensajes o enviar los mensajes a una cola dead-letter. En este ultimo caso, se debe contar con una estrategia para tratar dichos mensajes.
