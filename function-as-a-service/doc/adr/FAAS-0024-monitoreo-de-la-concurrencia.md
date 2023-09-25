# ADR FAAS 0024. Monitoreo de la concurrencia

Date: 2023-03-22

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, limite, concurrencia, escalamiento, monitoreo.

## Status

Accepted

Referenced by [ADR FAAS 0022. Definición del limite de concurrencia](FAAS-0022-definicion-del-limite-de-concurrencia.md)

## Context

Una "función como un servicio" ayuda a optimizar los costos ya que no tiene que pagar por servidores inactivos. Si embargo, debido a que la tecnología sin servidor administra sus recursos de infraestructura, muchas métricas tradicionales como el uso de la CPU no se podrán capturar, dando como resultado nuevos tipos de métricas muy relacionadas con la eficiencia de la ejecución de las funciones.

La concurrencia es una de las medidas de la efectividad del uso de una función, ya que una ráfaga de peticiones podrían verse estrangulada por no poseer suficiente simultaneidad para procesar ese tráfico o, una desmesurada ejecución ocasionada por una anomalía podría ser permitida. 

## Decision

Observaremos el valor de la concurrencia de una "función como un servicio" para conocer las solicitudes entrantes y así, determinar el valor que mejor se adapta al caso de uso.

La observación de la concurrencia permite entender y planificar el escalado, permitiendo establecer alertas en consecuencia para procesar las solicitudes entrantes de manera más eficiente.

## Consequences

Requerimos una plataforma de ejecución de la solución sin servidor.

Establecer el mecanismo para recolectar estas métricas, ya que las mismas pueden estar disponibles automáticamente a través del herramienta de monitoreo de la plataforma en la nube, o podrían extraerse de los registros de la función.

Observar la concurrencia puede ayudarnos a optimizar las funciones y administrar sus costos.
