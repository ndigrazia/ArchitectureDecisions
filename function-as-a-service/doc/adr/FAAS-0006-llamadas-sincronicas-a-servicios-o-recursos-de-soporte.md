# ADR FAAS 0006. Llamadas sincrónicas a servicios o recursos de soporte

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, sincrónica, orquestador, orquestación.

## Status

Accepted

## Context

Cuando implementados una "función como un servicio", podemos desear realizar invocaciones sincrónicas y secuenciales a servicios o recursos de soporte para implementar sus dependencias de tareas. Sin embargo, este estilo de implementación aumenta el tiempo total de espera en las ejecuciones de la función y como consecuencia, el costo incurrido.

## Decision

No diseñaremos o implementaremos una "función como un servicio" con llamadas sincrónicas y secuenciales a servicios o recursos de soporte.

Por ejemplo, no deseamos implementar una función que llame sincrónicamente a un Servicio de Almacenamiento, quede a la espera de su respuesta y luego, como resultado, realice una llamada sincrónica a otro servicio de base de datos NoSQL.

Como vemos, no implementaremos llamadas sincrónicas entre recursos o servicios de soporte que dependan de los resultados de las peticiones previamente realizadas.

Llamadas sincrónicas y secuenciales entre servicios o recursos de soporte ocasiona un aumento en los costos de ejecución.

## Consequences

Desacoplaremos la invocación entre los servicios o recursos de soporte.

Diseñaremos una primera función que responda inmediatamente luego de invocar al servicio o recurso de soporte. El servicio o recurso, concluida su responsabilidad, invocará a una segunda función (mediante eventos), que ejecuta las acciones requeridas sobre el siguiente recurso. De esta manera, separamos las invocaciones sincrónicas y secuenciales entre servicios o recursos de soporte.

Este enfoque minimiza el tiempo de espera total en las ejecuciones de la "función como un servicio". Sin embargo, hace mas complejo el diseño de solución.

Se reduce el costo de facturación.
