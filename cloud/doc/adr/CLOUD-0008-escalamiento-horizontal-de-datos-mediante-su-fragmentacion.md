# ADR CLOUD 0008. Escalamiento horizontal de datos mediante su fragmentación

Date: 2022-10-31

## Keywords

cloud, fragmentación, escalamiento, horizontal. 

## Status

Accepted

References [ADR CLOUD 0007. Favorecimiento de consistencia eventual de datos](CLOUD-0007-favorecimiento-de-consistencia-eventual-de-datos.md)

## Context

Tener una fuente de datos ejecutándose sobre un solo nodo de procesamiento presenta inconvenientes con respecto al volumen de las consultas que pueden realizarse, al volumen de las actualizaciones que pueden efectuarse y a la capacidad de los datos que pueden almacenarse. Estos inconvenientes, provocados por la limitación de la capacidad del nodo, causan tiempos de espera o de respuestas inaceptables.

## Decision

Fomentamos el uso del mecanismo de fragmentación de datos para facilitar el escalamiento horizontal de la fuente de datos.

Mediante la fragmentación de los datos se puede superar las limitaciones de disponer un solo nodo como fuente de datos, al dividir la fuente de datos en múltiples nodos o instancias donde cada nodo almacenará un subconjunto del total de los datos.

La fragmentación de los datos mejora la escalabilidad y optimiza el rendimiento de las consultas.

## Consequences

La lógica necesaria para implementar la fragmentación se complejizará si el servicio de fragmentación no está integrado en la fuente de datos.

Establecer, de acuerdo a las definiciones del negocio, como se realizará la fragmentación de los datos en los nodos, ya que las necesidades del negocio deberían ser satisfechas desde un nodo/fragmento por vez.

El uso del mecanismo de fragmentación puede complejizar la lógica usada para la selección y actualización de los datos.
