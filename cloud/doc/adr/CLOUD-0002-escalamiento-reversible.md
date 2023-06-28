# ADR CLOUD 0002. Escalamiento reversible

## Keywords

cloud, escalamiento, horizontal, reversible, aplicación, diseño, nodo, desarrollo.

## Status

Accepted

Referenced by [ADR CLOUD 0001. Escalamiento horizontal](CLOUD-0001-escalamiento-horizontal.md)

## Context

Cuando se escala horizontalmente, se agregan nodos a los nodos del clúster. Como resultado de este proceso, se produce un incremento en más recursos (como RAM, vCPU) en el clúster y así, se logra un incremento en el rendimiento de las aplicaciones, dando al negocio la ventaja de poder adaptarse a sus necesidades. Sin embargo, cuando los recursos asociados a la aplicación comienzan a quedar ociosos debido a la falta de carga de la aplicación, la eliminación de esos recursos inactivos permite ahorrar dinero.

## Decision

Liberaremos nodos o instancias (recursos) que previamente fueron requeridos por la aplicación durante los momentos de mayor tranquilidad.

Históricamente, la escalabilidad ha consistido en agregar capacidad y dado que, es relativamente difícil calcular la cantidad precisa de los recursos que necesita una aplicación, siempre ha sido más seguro la sobre-provisión. Sin embargo, en muchos casos esta capacidad extra no es aprovechada cuando no es utilizada por la aplicación que la solicito. En las aplicaciones modernas es mucho más fácil emplear esta capacidad extra devolviendo estos recursos a la plataforma para luego, cuando la necesidad lo requiera, volver a usarlos nuevamente. De esta manera, al hacer reversible los recursos solicitados podemos beneficiarnos de una mejora en el uso de los mismos y en los costos operativos.

## Consequences

Diseñar y desarrollar de aplicaciones teniendo presente la elasticidad de los recursos.
