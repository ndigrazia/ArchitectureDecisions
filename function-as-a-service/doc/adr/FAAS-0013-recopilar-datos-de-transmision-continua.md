# ADR FAAS 0013. Recopilar datos de transmisión continua

## Keywords

faas, serverless, función, sin servidor, servicio, datos, recopilar, ETL, extracción, transformación, streaming, carga, caso uso.

## Status

Accepted

References [ADR FAAS 0008. Patrones de carga predecibles](FAAS-0008-patrones-de-carga-predecibles.md)

## Context

Permanentemente las organizaciones deben recopilar datos de varias fuentes y en varios formatos, procesarlos y moverlos a almacenes de datos. A menudo es necesario darle forma a los datos antes de cargarlos en el destino final, el cual puede ser diferente a la fuente de origen.

La extracción, transformación y carga (ETL) es una técnica que permite obtener datos de diversas fuentes, darle formato según las reglas del negocio para luego, almacenarlos en un repositorio destino.

Actualmente las aplicaciones modernas gozan de la capacidad de generar datos continuamente (streaming de datos) desde diversas fuentes. El procesamiento de esos datos resulta beneficioso en la mayoría de las situaciones, haciendo al uso de la técnica de ETL una de las alternativas para la recolección y el tratamiento de los datos generados.

Dado que las soluciones sin servidor son ideales para streaming, se puede pensar que sería ideal implementar este caso de uso con una "función como un servicio" encargada del proceso de extracción, transformación y carga.

## Decision

Usaremos una "función como un servicio" para realizar la tarea de extracción, transformación y carga de datos generados de manera impredecible.

Configuramos o registramos una función para consumir los datos generados (extraer). Dicha función contiene lógica de filtrado, de validación, de normalización o cualquier otra lógica basada en reglas del negocio (transformar). Finalmente, el resultado de la fase de tratamiento de los datos, es enviado a otro lugar para su almacenamiento y/o procesamiento posterior (carga).

El destino final de los datos puede ser un repositorio centralizado diseñado para almacenar grandes cantidades de datos estructurados, semiestructurados o no estructurado (data lake).

## Consequences

Requerimos configurar o registrar sobre la plataforma la función que consumirá los datos generados.

Requerimos una plataforma de ejecución de la solución sin servidor.

Requerimos una solución de procesamiento de datos con alta performance y alta disponibilidad.
