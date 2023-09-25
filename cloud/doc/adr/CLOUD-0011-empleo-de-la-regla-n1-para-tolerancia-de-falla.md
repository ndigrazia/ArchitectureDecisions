# ADR CLOUD 0011. Empleo de la regla N+1 para tolerancia de falla

Date: 2022-11-07

## Keywords

cloud, tolerancia, falla, servicios.  

## Status

Accepted

## Context

Un sistema tolerante a fallas es aquel que continúa funcionando correctamente al momento de experimentar una falla en algunos de sus componentes.

Las aplicaciones modernas se organizan en cluster de varios nodos, asegurando que la falla en alguno de sus nodos no afecte el comportamiento de la aplicación, ya que si la aplicación fuera desplegada en una única instancia, la perdida del nodo afectaría negativamente la experiencia del usuario.

Asumiendo que ocurrirán fallas en los nodos y que debemos tomar medidas proactivas para garantizar que esas fallas no provoquen inactividad en la aplicación, nos preguntamos: ¿Cuántos de nodos se necesitan para una alta disponibilidad?. 

## Decision

Mantenemos una capacidad de tolerancia de fallas usando la regla N+1.

Si N nodos se necesitan para satisfacer la demanda de los usuarios, implementar N+1 nodos. Un nodo puede fallar o ser interrumpido sin impacto en la aplicación.

Las aplicaciones deberían permanecer disponible ante fallas en los nodos o las instancias sobre las cuales se entra ejecutándose mediante la implementación de medidas proactivas que garanticen que las fallas no provoquen tiempo de inactividad en la aplicación. Una medida proactiva es aplicar la regla N+1 que garantiza que un nodo pueda fallar o interrumpirse sin afectar las demandas de la aplicación. Esta regla establece que si se necesitan N nodos para soportar la demanda del usuario, se deben desplegar N+1 nodos.

No contar con un esquema de N+1 cuando ocurra una falla o interrupción en un nodo, provocará que el servicio tenga una capacidad reducida hasta que se haya implementado por completo el nuevo nodo. Esta perdida de rendimiento se debe a que existe un tiempo entre la ocurrencia de la falla y el reconocimiento parte del sistema de monitoreo de la plataforma en la nube.

## Consequences

Redundancia de los recursos.

Realizar un análisis detallado de las necesidades del negocio o fallas usuales para delimitar el tamaño de buffer de tolerancia de fallas y a cuáles capas de la arquitectura se le aplicará la regla N+1.
