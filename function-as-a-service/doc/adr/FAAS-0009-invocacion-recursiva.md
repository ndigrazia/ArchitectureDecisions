# ADR FAAS 0009. Invocación recursiva

Date: 2023-03-09

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, recursiva, recursivo, recursión.

## Status

Accepted

References [ADR FAAS 0022. Definición del limite de concurrencia](FAAS-0022-definicion-del-limite-de-concurrencia.md)

## Context

La recursión es un concepto en ciencias de la computación en donde una función se llama a sí misma, es decir, sostiene que resolver un problema se basa de obtener soluciones de instancias mas pequeñas del mismo problema.

La técnica de recursión nos ayuda a aprovechar el poder de cómputo de recursos de ejecución basados en contenedores o máquinas virtuales, ya que nos permite maximizar el uso de CPU. Sin embargo, en la solución de "función como un servicio", los costos dependen del tiempo de ejecución y de las invocaciones realizadas, haciendo que el uso de la recursión pueda provocar efectos indeseables debido a las capacidades de escalabilidad propias de las funciones.

Una función que se llama así misma continuamente, puede conducir a una ráfaga exponencial de invocaciones, ocasionando una explosión en los costos cobrados por parte del proveedor de la nube.

## Decision

Evitaremos implementar una "función como un servicio" que se llame asi misma.

## Consequences

Implementaremos una "función como un servicio" previniendo el uso de algoritmos recursivos al crear aplicaciones sin servidor.

Para los casos de negocio que requieran el uso de operaciones recursivas para ser resueltos debemos:

- Asegurar de realizar pruebas rigurosas para evitar bucles infinitos.
  
- Pasar datos entre las invocaciones para mantener un conteo de recurrencias y usarlo para detener la función en ejecución cuando el conteo de recurrencias alcanza un número determinado. El límite de recurrencias puede ser modificado de acuerdo al costo u otros factores.

- Configurar el límite de escalamiento de la función.

- Crear alarmas para monitorear el escalamiento de una función y así, recibir alertas si el escalamiento aumenta repentinamente.
