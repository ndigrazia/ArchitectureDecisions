# ADR CLOUD 0007. Favorecimiento de consistencia eventual de datos

Date: 2022-10-31 

## Keywords

cloud, consistencia, eventual.

## Status

Accepted

Referenced by [ADR CLOUD 0008. Escalamiento horizontal de datos mediante su fragmentación](CLOUD-0008-escalamiento-horizontal-de-datos-mediante-su-fragmentacion.md)

## Context

El teorema Brewer establece tres garantías para datos almacenados en forma distribuida en más de un nodo.

La primer garantía, Consistencia (Consistency), establece que todas las lecturas obtienen las mismas respuestas. La segunda garantía, Disponibilidad (Availability), determina que las consultas siempre reciben una respuesta. Es decir, acceso continuo a los datos, incluso si hay una falla parcial del sistema. Por último, la tercer garantía, Tolerancia de Partición (Partition tolerance), define que siempre el sistema continúa operando, incluso si los nodos está desconectados de la red y no pueden comunicarse. Según este teorema, dentro de un contexto de datos distribuidos solamente pueden implementarse dos de las tres garantías. Es decir, puede realizarse combinaciones en dos de cualquiera de las tres garantías, teniendo presente que cada una de estas combinaciones producirá comportamientos muy diferentes.

## Decision

Proporcionamos la consistencia eventual de los datos para favorecer un escalamiento más eficiente.

Dado que en los ambientes de datos distribuidos la Tolerancia de Partición es necesaria, no podemos garantizar tanto la Consistencia como la Disponibilidad al mismo tiempo. Una compensación muy recomendada es permitir una eventual consistencia de datos a favor de una mejor escalabilidad, garantizando de esta manera dos de las tres garantías del teorema de Brewer: Tolerancia de Partición y Disponibilidad.

Es importante, determinar los escenarios del negocio para establecer si datos eventualmente consistentes pueden ser empleados.

## Consequences

Evaluar como la fuente de datos implementa el mecanismo de consistencia eventual para determinar los escenarios de actualización o de lectura de datos que no son inmediatamente consistentes.

Diseñar las aplicaciones para reflejar, para el caso de usuarios que necesitan datos actualizados, el cambio realizado recientemente por el propio usuario sin volver a cargar los datos desde la fuente de datos, ya que los mismos podrían estar obsoletos.

