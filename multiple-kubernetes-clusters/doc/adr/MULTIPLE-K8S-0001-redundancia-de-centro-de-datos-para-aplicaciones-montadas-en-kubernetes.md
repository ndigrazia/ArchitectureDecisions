# ADR MULTIPLE-K8S 0001. Redundancia de centro de datos para aplicaciones montadas en kubernetes

Date: 2022-10-06

## Keywords

redundancia, alta disponibilidad, centro de datos, zonas, kubernetes.

## Status

Accepted

References [ADR CLOUD 0013. Disposición cercana de los nodos o instancias](../../../cloud/doc/adr/CLOUD-0013-disposicion-cercana-de-los-nodos-o-instancias.md)

## Context

El cluster Kubernetes brinda a las aplicaciones ejecutadas sobre dicha plataforma muchas funciones de soporte, entre ellas la posibilidad de reiniciar, de reemplazar y de reprogramar sus servicios cuando los nodos donde se ejecutan sufran inconvenientes. Sin embargo, si el despliegue del cluster se realiza en un único centro de datos, conteniendo su propia energía y conectividad de red, cualquier inconveniente en el mismo puede afectar la disponibilidad de los servicios ejecutados en la plataforma.

## Decision

Usaremos redundancia de centro de datos para los servicios ejecutados sobre kubernetes, de tal manera que los servicios de las aplicaciones se puedan implementar y diseñar de modo que si falla un centro de datos, las instancias del otro centro de datos se activen y continúen el trabajo de los servicios del centro de datos fallido.

La redundancia de centro de datos para los servicios de las aplicaciones montados en kubernetes tiene como objetivo mejorar la alta disponibilidad.

La redundancia es requerida para ambientes productivos pero sugerida para ambientes de desarrollo o ambientes de control (devops) de acuerdo al presupuesto disponible.

## Consequences

Los centros de datos participantes deben estar conectados entre sí a través de enlaces de red privada de baja latencia.

La redundancia de centro de datos depende de la solución que se quiere soportar en la plataforma. Algunas tecnologías, basadas en quorum, requieren de un mínimo de instancias desplegadas en los diferentes centros de datos, determinando así, la cantidad de centro de datos necesarios para garantizar la alta disponibilidad del servicio.
