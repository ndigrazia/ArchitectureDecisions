# ADR CLOUD 0013. Disposición cercana de los nodos o instancias

Date: 2022-11-07

## Keywords

cloud, nodo, cercanía, latencia, reducción.

## Status

Accepted

Referenced by [ADR MULTIPLE-K8S 0001. Redundancia de centro de datos para aplicaciones montadas en kubernetes](../../../multiple-kubernetes-clusters/doc/adr/MULTIPLE-K8S-0001-redundancia-de-centro-de-datos-para-aplicaciones-montadas-en-kubernetes.md)

References [ADR CLOUD 0014. Reducción de la latencia de la red](CLOUD-0014-reduccion-de-la-latencia-de-la-red.md)

## Context

Las plataformas en la nube suelen brindar muchos centros de datos, permitiendo a la aplicación utilizar los servicios ofrecidos por la plataforma en cualquiera de esos centros de datos.

La posibilidad de tener múltiples centros de datos ofrece grandes ventajas, pero también, presenta el riesgo cuando los componentes que utilizan las aplicaciones son distribuidos incorrectamente, comprometiendo el desempeñó de la aplicación, ya que el intercambio de datos (distancia recorrida por los datos) entre los nodos o instancias no ocurre instantáneamente. El tiempo involucrado en transmitir los datos se conoce como latencia de red.

A medida que la distancia mantenida entre los nodos de la aplicación aumenta, aumenta también la latencia de la red, degradando la experiencia de usuario y aumentando los costos del tráfico.

## Decision

Favoreceremos la disposición cercana de los nodos que interactúan frecuentemente.

A mayor distribución de los nodos, mayor impacto. 

El favoreciendo de la cercanía de los nodos mejora la latencia en las respuestas de las solicitudes y como consecuencia, mejora la experiencia del usuario.

La latencia percibida puede ser reducida por medio de:

- Desplegar los nodos de aplicaciones complejas, conformadas por múltiples capas
y que involucran varios centros de datos, en una misma ubicación, considerando
la frecuencia de interacción entre ellos como medida de agrupamiento.

- Automatizar el despliegue para evitar errores en la asignación de los nodos a
centro de datos incorrectos.

## Consequences

Aumenta la complejidad de la solución a medida que aumenta la cantidad de centro de datos usados por la aplicación.
