# ADR CLOUD 0004. Uso de nodos autónomos o independientes

Date: 2022-10-26

## Keywords

cloud, escalamiento, horizontal, reversible, nodo, independiente, autónomo.

## Status

Accepted

References [ADR CLOUD 0003. Empleo de nodos homogéneos](CLOUD-0003-empleo-de-nodos-homogeneos.md)

Referenced by [ADR CLOUD 0001. Escalamiento horizontal](CLOUD-0001-escalamiento-horizontal.md)

## Context

Alcanzar un escalado horizontal eficiente significa agregar más instancias para soportar la carga de trabajo de la aplicación, contar con instancias con las mismas características homogéneas y la posibilidad de que cada nodo adicional opere o no independientemente del resto de los nodos que componen a una capa o función.

## Decision

Realizaremos escalamiento horizontal con nodos autónomos e independientes.

Dentro de una capa o una funcionalidad determinada (como un servidor web) los nodos o instancias deben operan de forma autónoma, independientes entre sí. Es decir, el nodo no debe necesitar comunicarse con otros nodos similares para realizar su trabajo.

La autonomía es importante para que los nodos puedan mantener su propia eficiencia, independientemente de lo que estén haciendo otros nodos. Esto significa que el éxito del escalamiento horizontal está en la posibilidad de incrementar las capacidades de una aplicación mediante la adición de nodos autónomos con la misma cantidad de capacidad usable.

## Consequences

Diseñar las aplicaciones de manera tal que los nodos dentro de la misma capa o función operen de forma autónoma e independientes entre sí.
