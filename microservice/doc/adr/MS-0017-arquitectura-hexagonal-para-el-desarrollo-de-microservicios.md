# ADR MS 0017. Arquitectura hexagonal para el desarrollo de microservicios

Date: 2022-12-14

## Keywords

microservicio, hexagonal, arquitectura.

## Status

Accepted

References [ADR MESH 0001. Uso de sidecar para acoplamiento operativo](../../../mesh/doc/adr/MESH-0001-uso-de-sidecar-para-acoplamiento-operativo.md)

## Context

Un estilo arquitectónico en software, al igual que un estilo de arquitectura edilicia, proporciona un conjunto de elementos (componentes) y sus relaciones (conectores) a partir de los cuales, se puede construir la aplicación o el servicio basado en el conjunto de conceptos, valores, técnicas y procedimientos definidos por el estilo arquitectural.

El ejemplo clásico de un estilo arquitectónico es la arquitectura en capas. Una arquitectura en capas organiza los componentes de software en capas. Cada capa tiene un conjunto bien definido de responsabilidades y solo puede depender de la capa inmediatamente debajo de ella (si es una capa estricta) o de cualquiera de las capas debajo de ella.

Los desarrollos más modernos utilizan arquitecturas basadas en descomposición por dominós de negocios que ayudan a superar varios inconvenientes presentados en arquitecturas más clásicas.

La arquitectura hexagonal es una alternativa al estilo arquitectónico en capas.

## Decision

Implementaremos una arquitectura hexagonal en el desarrollo de microservicios.

El estilo de arquitectura hexagonal coloca la lógica de negocio en el centro. Se usan uno o más adaptadores entrantes para manejar solicitudes desde el exterior a la lógica de negocios. Y de manera similar, uno o más adaptadores de salida para que la lógica de negocio pueda comunicarse con el exterior. Esta característica hace que la lógica de negocio no se mezcle con la lógica requerida para la comunicación hacia o desde el exterior.

La lógica de negocio tiene una o más interfaces, llamadas puertos. Un puerto define un conjunto de operaciones usadas por la  lógica del negocio para interactuar con lo que está fuera de ella. Hay dos tipos de puertos: puertos de entrada y de salida. 

Un puerto de entrada es una interfaz que expone métodos públicos, implementados por la lógica de negocio e invocados por las aplicaciones externas. Un puerto de salida es una interfaz que expone métodos invocados por la lógica de negocio.

Al igual que con los puertos, hay dos tipos de adaptadores: entrantes y salientes. Un adaptador de entrada maneja las solicitudes del mundo exterior invocando un puerto de entrada. Un adaptador de salida implementa un puerto de salida y maneja las solicitudes hacia una aplicación o servicio externo (base de datos o broker de mensajería).

Los adaptadores son componentes que permiten modificar la lógica de acceso a los recursos externos sin tener que realizar cambios en la lógica de negocio dependiente.

## Consequences

Requerimos la implementación de los componentes que conforman la arquitectura hexagonal.

Un beneficio importante del estilo arquitectónico hexagonal es que desacopla la lógica de negocio de la lógica de acceso hacia o desde servicios externos en los adaptadores, permitiendo su evolución (protocolo de comunicación, librerías, tecnologías, etc) de forma aislada a la lógica del negocio. Este estilo de arquitectura refleja con mayor precisión la arquitectura de una aplicación o servicio moderno.

La construcción de servicios pensados en una arquitectura hexagonal suele complejizar el desarrollo debido a que es necesario la implementación de varios componentes con responsabilidades claramente establecidas. Sin embargo, dado las ventajas que presenta en la adaptación de los servicios a los cambios del negocio vale la pena su implementación.

Otra alternativa es encapsular la lógica de interacción con el exterior mediante el uso de un componente de sidecar.
