# ADR CLOUD 0010. Tratamiento de respuestas "servicio ocupado"

## Keywords

cloud, integración, respuesta, recursos, servicios, ocupado.  

## Status

Accepted

References [ADR CLOUD 0009. Detección de respuestas de "servicio ocupado"](CLOUD-0009-deteccion-de-respuestas-de-servicio-ocupado.md)

## Context

Identificar los escenarios dentro de la aplicación donde pueden ocurrir fallas transitorias o señales de ocupado es el primer paso en logar un sistema estable. No contar con tratamiento de esas fallas transitorias o eventos de “servicio ocupado” afectará a la experiencia del usuario, al no poder mitigar las fallas en la aplicación.

## Decision

Proporcionaremos lógica para el tratamiento de respuestas “servicio ocupado” a los pedidos realizados sobre servicios en la plataforma en la nube.

Los detalles de como manejar estos tipos de errores son específicos para cada aplicación, es decir la elección de si se reintenta, el numero de reintentos y el tiempo entre los reintentos dependerán de si hay un usuario esperando por un resultado o si se trata de una operación por lotes. Finalmente, luego de un tiempo razonable o números de reintentos, la aplicación deberá responder ante este escenario dando una respuesta insatisfactoria, por ejemplo retornando una excepción o una respuesta establecida por el negocio.

Existen varios patrones de estabilidad que brindan una guía de diseño para reducir, eliminar o mitigar los efectos indeseables de las fallas de sistema. Aplicando tratamiento de fallas transitorias se permite sabiamente reducir el daño. 

Los patrones de estabilidad que podemos emplear para el tratamiento de fallas de la aplicación son:

    - Timeout.
    - Circuit Breaker.
    - Bulkheads.
    - Fail Fast.
    - Back Pressure.
    - Governor.
    - Shed load.
    - Let it Crash.
    - Steady State.

## Consequences

Complejidad en el desarrollo y en el diseño de la aplicación, ya que se requiere lógica para el tratamiento de fallas transitorias o señales de ocupado:

    - Establecer políticas de reintentos (inmediata, temporal o en incrementos) antes de considerar la respuesta como invalida.
  
    - Establecer cantidad de reintentos.
  
    - Lanzar una excepción si el servicio aún no responde luego, de una cantidad razonable de reintentos y retrasos.
  
    - Aplicar patrones de estabilidad para mitigar los problemas de puntos de integración.
