# ADR CLOUD 0012. Finalización limpia de un modo o instancia

## Keywords

cloud, tolerancia, falla, servicios, nodo, limpieza, limpia, finalización.

## Status

Accepted

## Context

Podemos manejar de manera responsable el cierre del nodo. No todas las fallas de hardware
pueden dar como resultado una falla del nodo. Las plataformas en la nube pueden detectar señales de que el hardware tiene una falla y en consecuencia, pueden iniciar de manera preventiva un cierre controlado de un nodo, moviendo los servicios u operaciones a otro nodo diferente.

Independientemente de la razón por la que el nodo es liberado, es importante permitir que el trabajo sea completado, sin afectar negativamente la experiencia del usuario.

Las plataformas en la nube proporcionan señales para que las aplicaciones sepan que un nodo está a punto de ser cerrado.

## Decision

Proporcionaremos lógica para la finalización ordenada y controlada de un nodo o una instancia.

Una vez que un nodo o una instancia es seleccionado para ser liberado debido a sucesivas fallas, ya sea de hardware o de software, la plataforma en la nube debe realizar una serie de acciones tendiendo a retirar el componente afectado: Procederá a eliminar la instancia del balanceador de carga para que no se le dirijan nuevas solicitudes. Luego, enviará una serie de señales para indicar la liberación de la instancia. Estas señales le permiten al componente afectado poder realizar acciones (liberación de recursos) que tienden a evitar la pérdida de datos y la degradación de la experiencia del usuario. Finalmente, se procederá a la liberación de la instancia cuando haya finalizado el tiempo otorgado para un cierre ordenado. 

Generalmente, no hay demasiada lógica al momento de liberar una instancia o nodo sin estado.

## Consequences

Complejidad en el desarrollo y en el diseño de la aplicación, ya que requiere identificar que señales son enviadas por la plataforma en la nube al momento de realizar la liberación de una instancia o de un nodo. Y Luego, determinar si se requieren de funciones de finalización y en caso de ser necesarias, establecer la lógica adecuada para terminar ordenadamente el nodo o la
instancia.
