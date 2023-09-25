# ADR FAAS 0002. Orquestador

Date: 2023-02-28

## Keywords

faas, serverless, función, sin servidor, orquestador, orquestación, servicio.

## Status

Accepted

Referenced by [ADR FAAS 0004. Ejecución sincrónica de comandos sobre otras funciones](FAAS-0004-ejecucion-sincronica-de-comandos-sobre-otras-funciones.md)

References [ADR FAAS 0021. Ruteador](FAAS-0021-ruteador.md)

## Context

Varios de los procesos en una organización requieren de flujos de trabajos complejos. Un proceso de negocio representa una serie de actividades o de tareas donde la ejecución de una determinada operación depende de múltiples estados de sus variables o de diversas situaciones complejas.

El uso de una "función como un servicio" para implementar el control de los procesos de negocio ocasiona que su código sea difícil de leer, de comprender y de mantener, debido a que no solo debe implementar la lógica del proceso de negocio, sino que también, debe tratar el manejo de errores, la lógica de reintento y el procesamiento de las comunicaciones de entradas y de salidas.

## Decision

No usaremos "función como un servicio" para orquestar complejos flujos de trabajo de un proceso de negocio. 

Como alternativa, al uso de "función como un servicio", utilizaremos servicios cuyo objetivo sea orquestar estos flujos de trabajo mediante una máquina de estado como por ejemplo, Logic App en Azure o Step Functions en AWS. Además, estos servicios están pensados para mantener diferentes versiones de flujos de trabajo, reduciendo la cantidad de código de implementación, asiendo más fácil su prueba y su mantenimiento.

Cuando la coordinación de actividades es simple podemos emplear un Ruteador para reducir los costos de implementación.

## Consequences

Emplearemos herramientas o servicios orientados y pensados en crear y en ejecutar flujos de trabajo complejos con múltiples tipos de fallas y lógica de reintento. 

Los servicios pueden ser provistos por el proveedor en la nube o por software de tercero.

Los beneficios de no orquestar flujos de trabajo en "función como un servicio" son:

- Código bien estructurado, ya que la lógica de orquestación puede generar "código espagueti" que es difícil de leer, comprender y mantener.

- Servicios con una única responsabilidad, la cual está claramente definida.

Finalmente, se requiere conocimiento y administración de los servicios o herramientas que gestionen los flujos de trabajo.
