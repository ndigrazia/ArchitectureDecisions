# ADR CLOUD 0001. Escalamiento horizontal

## Keywords

cloud, escalamiento, horizontal, aplicación, diseño, nodo, desarrollo.

## Status

Accepted

References [ADR CLOUD 0002. Escalamiento reversible](CLOUD-0002-escalamiento-reversible.md)

References [ADR CLOUD 0003. Empleo de nodos homogéneos](CLOUD-0003-empleo-de-nodos-homogeneos.md)

References [ADR CLOUD 0004. Uso de nodos autónomos o independientes](CLOUD-0004-uso-de-nodos-autonomos-o-independientes.md)

References [ADR CLOUD 0005. Escalamiento horizontal con nodos sin estado](CLOUD-0005-escalamiento-horizontal-con-nodos-sin-estado.md)

References [ADR CLOUD 0006. Escalamiento elástico y automático basado en reglas](CLOUD-0006-escalamiento-elastico-y-automatico-basado-en-reglas.md)

Referenced by [ADR DEVOPS 0008. Escalamiento automático de la plataforma de flujo continuo](../../../devops/doc/adr/DEVOPS-0008-escalamiento-automatico-de-la-plataforma-de-flujo-continuo.md)

## Context

La escalabilidad de una aplicación es la posibilidad de que sus servicios se adapten al aumento de su carga. Existen dos formas de escalar una aplicación: el escalado vertical y el escalado horizontal. El primero implica el aumento de la capacidad de un recurso (como RAM, vCPU) de un nodo. El segundo, consiste en agregar nuevas instancias o nodos.

## Decision

Aumentaremos la capacidad de crecimiento o de rendimiento de la aplicación aprovechando el escalamiento horizontal mediante el agregado de nodos o de instancias.

Tradicionalmente, el mecanismo de escalamiento clásico ha sido el escalamiento vertical, el cual consiste en aumentar la capacidad o el poder individual del nodo mediante mejoras en el hardware. Esta estrategia fue ampliamente utilizada debido a su bajo riesgo de implementación, ya que se puede realizar sin necesidad de efectuar cambios en la aplicación. Sin embargo, es limitada dado que no siempre se puede disponer del hardware necesario para satisfacer la demanda de la aplicación y aun, cuando es posible contar con los recursos necesarios, puede ocurrir que el software no fue pensado para obtener las ventajas del nuevo hardware. Claramente, el enfoque del escalamiento horizontal es diferente al enfoque vertical al buscar aumentar la capacidad de la aplicación mediante la adición de nodos, permitiendo ofrecer una escala de crecimiento que supera a las posibilidades ofrecidas con el escalado vertical.

El escalado horizontal presenta ventajas sobre el escalado vertical:

- Las aplicaciones desarrolladas para aprovechar esta capacidad pueden ejecutarse en varios nodos, con lo que se alcanzan escalas que no son posibles en un solo nodo.
  
- El escalamiento horizontal permite no solamente agregar más instancias sino quitar instancias.
  
- Puede ser automatizado.

- Mejora la capacidad de respuesta de la aplicación ante fallas.

## Consequences

Diseñaremos y desarrollaremos aplicaciones concurrentes y distribuidas para aprovechar al máximo el procesamiento de varios nodos.

El desarrollo y diseño de aplicaciones distribuidas presenta una mayor complejidad al diseño de aplicaciones monolíticas.

Posibilidad de cuello de botella en los elementos con estado de un sistema (como las bases de datos).
