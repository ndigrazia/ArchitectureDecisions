# ADR CLOUD 0003. Empleo de nodos homogéneos

Date: 2022-10-26

## Keywords

cloud, escalamiento, horizontal, reversible, nodo, homogeneo.

## Status

Accepted

Referenced by [ADR CLOUD 0004. Uso de nodos autónomos o independientes](CLOUD-0004-uso-de-nodos-autonomos-o-independientes.md)

Referenced by [ADR CLOUD 0001. Escalamiento horizontal](CLOUD-0001-escalamiento-horizontal.md)

## Context

El escalamiento horizontal consiste en disponer una serie de nodos con el objetivo de trabajar en conjunto para otorgar mayores capacidades y resiliencias a las aplicaciones. Sin embargo, las características que presenten esos nodos o instancias también tienen implicancia directa en el rendimiento y en el uso eficiente de los recursos, ya que si los mismos tuvieran capacidades diferentes, el proceso de la distribución de la carga y el uso eficiente de los recursos se complicaría.

## Decision

Realizaremos el escalamiento horizontal con instancias o nodos homogéneos, por funcionalidades o por capas.

Las aplicaciones diseñadas para escalamiento horizontal generalmente están separadas por funciones o por capas. Por ejemplo, una aplicación puede tener nodos de servidor web y nodos de servicio de facturación. A la hora de aumentar la capacidad de una aplicación pensamos en agregar uno o más nodos para una función o una capa específica. Esto es: un servidor web o un servicio de facturación. Decimos que los nodos son homogéneos cuando los nodos, pertenecientes a una función o capa específica, están configurados de forma idéntica. 

Contar con nodos homogéneos simplifica el escalado horizontal. Si los nodos son homogéneos, entonces el balanceo de carga es más simple, la planificación de la capacidad es más fácil y es más fácil escribir reglas para el escalado automático. De lo contrario, el proceso de distribución de los pedidos no es eficiente.

## Consequences

Diseñar nodos con configuraciones idénticas dentro de la misma capa o función. Es decir, con los mismos recursos de hardware (usualmente virtual), el mismo sistema operativo y el mismo software de función específica.

