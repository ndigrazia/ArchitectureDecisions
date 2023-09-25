# ADR MSG 0002. Procesamiento idempotente para mensajes almacenados en una cola de mensajería

Date: 2022-08-22

## Keywords

messaging, message, asincrónica, idempotente, mensaje, cola.

## Status

Accepted

## Context

Los mensajes almacenados en una cola de mensajería son removidos para su posterior tratamiento. Cuando un mensaje se remueve de la cola no se elimina definitivamente (client acknowledge mode), sino que es ocultado durante un periodo de tiempo haciendo que el mensaje no esté disponible para ser procesado simultáneamente por otro servicio. Puede ocurrir, por algún motivo, que un mensaje no sea procesado totalmente, haciendo que el mismo quede disponible en la cola para continuar con su procesamiento. Cualquier mensaje que es procesado por segunda vez puede traer inconvenientes, ya que muchas de las actividades realizadas en su procesamiento no requieren ser ejecutadas nuevamente. 

## Decision

Desarrollamos algoritmos para procesamiento idempotente para los mensajes almacenados en una cola de mensajería.

El procesamiento idempotente garantiza que el mensaje puede procesarse varias veces y aun así conseguir el mismo resultado que se obtendría si se realizase una sola vez, garantizando la estabilidad y la confiabilidad de la aplicación.

## Consequences

Requerimos definir una variable de conteo que permite conocer la cantidad de veces que un mensaje es tratado en la cola de mensajería (muchos servicios de mensajería disponen de una variable para esta función) y, desarrollar lógica adicional para apoyar la idempotencia para mensajes con intentos repetidos de procesamiento. 

Evaluar el uso de estados para determinar el estado del mensaje y así, determinar la proxima actividad a realizar en su procesamiento.
