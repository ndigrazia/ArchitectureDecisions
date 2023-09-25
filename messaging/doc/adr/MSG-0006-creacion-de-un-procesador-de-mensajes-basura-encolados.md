# ADR MSG 0006. Creación de un procesador de mensajes basura encolados

Date: 2022-08-24

## Keywords

messaging, message, asincrónica, mensaje, cola, tratamiento, procesamiento, basura.

## Status

Accepted

Referenced by [ADR MSG 0003. Eliminación de mensajes basura encolados](MSG-0003-eliminacion-de-mensajes-basura-encolados.md)

References [ADR MSG 0005. Definición del tamaño de la cola de mensajería](MSG-0005-definicion-del-tamano-de-la-cola-de-mensajeria.md)

Referenced by [ADR FAAS 0004. Ejecución sincrónica de comandos sobre otras funciones](../../../function-as-a-service/doc/adr/FAAS-0004-ejecucion-sincronica-de-comandos-sobre-otras-funciones.md)

## Context

Durante el procesamiento del mensaje pueden surgir errores que conducen al consumidor a no poder tratar dicho mensaje, ya que carece de la posibilidad de hacerlo. Esta situación resulta en un mensaje basura que, para poder resolver, el consumidor o el propio sistema de mensajería (broker) debe enviarlo a otra cola.

La cola de mensajes, comúnmente llamada dead-letter o cola de mensajes fallidos, contiene los mensajes no tratados, los cuales deben ser procesados, ya que de lo contrario se acumularan hasta alcanzar el límite máximo de la cola. Un procesador de mensajes basura asociado a la cola dead-letter debe reparar, almacenar o dar algún tratamiento a los mensajes.

## Decision

Establecemos e implementamos mecanismos para procesar mensajes basura encolados en colas de dead-letter.

La estrategia o el mecanismo para procesamiento de los mensajes existentes en la cola dead-letter varia según los requerimientos o definiciones del negocio.

Una buena estrategia para el tratamiento podría ser que el procesador, mediante programación sin intervención humana, pueda reparar el mensaje original, enviándolo de vuelta a su cola de origen. En caso de que el mensaje no pueda ser reparado, puede informar al humano para que se haga cargo del caso, lo repare manualmente y lo reenvíe a la cola original.

## Consequences

Requerimos desarrollar lógica adicional para un procesador de mensajes basura que intente averiguar porque no se pueden procesar los mensajes, analizando si el error es estático y determinista o, mediante el uso de algoritmos de machine learning, examinar la anomalía en sus datos.

Requerimos definir la lógica para reparar el mensaje y en el caso de que los mensajes no fueran reparados, establecer, de acuerdo a las definiciones del negocio, como tratarlos.

Tenga cuidado de no implementar mecanismos de reintentos que sobrecarguen su sistema.
