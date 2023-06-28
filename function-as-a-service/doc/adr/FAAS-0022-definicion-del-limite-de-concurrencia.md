# ADR FAAS 0022. Definición del limite de concurrencia

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, limite, concurrencia, escalamiento.

## Status

Accepted

Referenced by [ADR FAAS 0009. Invocación recursiva](FAAS-0009-invocacion-recursiva.md)

References [ADR FAAS 0026. Despliegue mediante pipeline](FAAS-0026-despliegue-mediante-pipeline.md)

References [ADR FAAS 0024. Monitoreo de la concurrencia](FAAS-0024-monitoreo-de-la-concurrencia.md)

## Context

La capacidad de escalamiento automático es uno de los principales beneficios del uso de una "función como un servicio", ya que permite que una función escale casi instantáneamente e independiente según la demanda
creciente o decreciente de peticiones.

La tasa de trafico enviado por una función, dado su potencial de crecimiento casi infinito, puede sobrecargar los recursos de soporte (por ejemplo, bases de datos), saturar los servicios ofrecidos en una VPC privada o incremento en los costos cobrados por parte del proveedor de la nube.

## Decision

Establecemos individualmente el limite máximo de concurrencia de una "función como un servicio".

Precisar este umbral permite estrangular la ejecución simultanea de funciones.

Generalmente los proveedores de la nube tienen un valor predeterminado para la ejecución simultanea de funciones a nivel de cuenta.

## Consequences

Requerimos una plataforma de ejecución de la solución sin servidor.

Determinaremos un valor numérico para el límite de concurrencia de una función.

Posiblemente, asignar un límite de simultaneidad para una función específica, reduce la cantidad disponibles de ejecuciones simultaneas a nivel de la cuenta.

Protección contra ráfagas exponenciales de invocaciones ocasionadas por fallas.
