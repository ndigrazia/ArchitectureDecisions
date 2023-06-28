# ADR CLOUD 0014. Reducción de la latencia de la red

## Keywords

cloud, nodo, cercanía, latencia, reducción.

## Status

Accepted

Referenced by [ADR CLOUD 0013. Disposición cercana de los nodos o instancias](CLOUD-0013-disposicion-cercana-de-los-nodos-o-instancias.md)

## Context

En la arquitectura distribuida los nodos, los servicios o los usuarios finales se comunican transmitiendo datos a traves de una red, haciendo que la latencia de la red (tiempo involucrado en transmitir) sea una variable a considerar.

El rendimiento y la escalabilidad de la aplicación se verán afectados si los datos tardan demasiado en llegar a la computadora del cliente. 

Los efectos de la latencia de la red también pueden variar según la ubicación geográfica: para algunos usuarios del sistema, puede parecer increíblemente rápido, mientras que para otros usuarios puede parecer lento.

## Decision

Favoreceremos la reducción de la latencia de la red usando técnicas que posibiliten su disminución.

Los servidores altamente escalables y de alto rendimiento no garantizan que la aplicación funcione correctamente debido a que en un ambiente distribuido la transmisión de datos a través de una red no ocurre instantáneamente (latencia), comprometiendo el desempeño de la aplicación. Dispositivos como enrutadores, conmutadores, puntos de acceso inalámbricos y tarjetas de red introducen sus propias latencias. La combinación de todos estas demoras produce el retraso total experimentado por los datos que tienen que viajar a través de la red.

El impacto de la latencia de la red puede verse minimizado mediante las siguientes técnicas:

- Compresión de datos en cache.

- Procesamiento en segundo plano donde las actualizaciones de la pantalla no ocurren hasta que llegan los datos.

- Recuperación predictiva, donde los datos se cargan previamente a la necesidad de los mismos.

- Acercar la aplicación a los usuarios.

- Acercar los datos de la aplicación a los usuarios.
  
- Asegurar que los nodos de nuestra aplicación estén juntos

## Consequences

Complejidad en el desarrollo y en el diseño de la solución.

Determinar la estrategia mas adecuada al negocio para favorecer la reducción de la latencia de la red.
