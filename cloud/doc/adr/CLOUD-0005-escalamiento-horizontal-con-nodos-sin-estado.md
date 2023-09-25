# ADR CLOUD 0005. Escalamiento horizontal con nodos sin estado

Date: 2022-10-28

## Keywords

cloud, escalamiento, horizontal, nodo, estado.

## Status

Accepted

Referenced by [ADR CLOUD 0001. Escalamiento horizontal](CLOUD-0001-escalamiento-horizontal.md)

## Context

Algunas aplicaciones usan sticky sessions para almacenar el contexto de invocación. A través de este mecanismo, se asigna al usuario a un nodo específico cuando este visita por primera vez a la aplicación. Una vez asignado, ese nodo satisface todas las solicitudes de ese usuario durante su interacción. 

Un servicio intermedio (balanceador de carga) es quien asegura que las peticiones de cada usuario sean dirigidas a su nodo asignado.

El almacenamiento de estado en los nodos puede degradar la experiencia del usuario. Si el nodo que administra el estado de la sesión desaparece, fuerza a que desaparezca también el estado de la sesión del usuario que lo acompaña, obligando al usuario a iniciar la sesión de nuevo.

## Decision

Realizaremos el escalamiento horizontal con nodos sin estado, almacenando el contexto o estado de la sesión por fuera del nodo.

Las aplicaciones diseñadas para escalamiento horizontal generalmente se ven beneficiadas por tener nodos o instancias sin estados (stateless). Esto significa que el contexto de invocación o sesión no es mantenido en los nodos de una petición a otra. Un nodo que mantiene el contexto de invocación es un posible punto de falla. Si el nodo falla, esos datos se pierden, ocasionando un impacto negativo en la experiencia del usuario, al verse forzado a repetir todas las operaciones previamente realizadas. Además, la falta de un nodo puede producir inconvenientes en la distribución de la carga, ya que los nuevos nodos no podrán asimilar las nuevas cargas al no contar con el contexto ya almacenado en otros nodos, perdiendo de esta manera la ventaja de la elasticidad de los recursos.

El desarrollo de aplicaciones modernas en la nube busca tener un contexto de invocación almacenado externamente es decir, por fuera de los nodos o instancias.

Los nodos sin estado facilitan el escalamiento de las aplicaciones.

## Consequences

Evitamos el uso de sticky sessions. 

La solución es mas compleja, ya que requiere de un componente externo que almacene la sesión del usuario.

Usaremos cookies para almacenar un identificador de sesión, permitiendo vincular el estado de la sesión del lado del servidor. Al emplear el identificador de sesión, los datos de la sesión pueden modificarse o recuperarse desde un recurso externo, como por ejemplo, un servicio de caché distribuida.

Mantener la capa de servicios independiente del contexto de invocación.

Almacenar en un recurso externo, no en el disco local de un nodo individual el contexto o estado de sesión.
