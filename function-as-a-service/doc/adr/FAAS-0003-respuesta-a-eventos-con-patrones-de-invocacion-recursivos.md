# ADR FAAS 0003. Respuesta a eventos con patrones de invocación recursivos

Date: 2023-03-01

## Keywords

faas, serverless, función, sin servidor, evento, servicio, invocación, llamada, recursivo, recursiva.

## Status

Accepted

## Context

Existen varias formas de invocar a una "función como un servicio", algunas de ellas son mediante una URL expuesta en un API Gateway, una interfaz de línea de comandos, en respuestas (eventos) a acciones o según un cronograma designado.

Con la llegada de las "funciones como un servicio", los proveedores de nube han adaptado sus plataformas parque que los eventos, antes usados para auditorias o seguimientos internos, puedan invocar a una función con lógica de negocio.

Podemos programar la invocación de las "funciones como un servicio" para manipular los eventos resultantes de las acciones realizadas sobre los servicios administrados por el proveedor de la nube. Sin embargo, como resultado de estas acciones, se pueden producir bucles infinitos ocasionados por respuestas a eventos que se retroalimentan.

## Decision

No diseñaremos o implementaremos servicios o recursos que generen eventos que realicen invocaciones cíclicas de "funciones como un servicio" entre ellos.

El servicio o recurso que invoca una función debe ser diferente del servicio o recurso al que genera la función; esto significa que no hay un camino directo que empiece y termine generando un evento que invoque a la misma función.

La generación de invocaciones cíclicas tiene el potencial de provocar más daño en  aplicaciones en la nube. Las funciones escalarán automáticamente de acuerdo al tráfico, por lo que el bucle puede hacer que se consuman más recursos que en aplicaciones tradicionales, llegando hasta consumir toda la capacidad de ejecución otorgada a las funciones.

## Consequences

Separaremos los recursos o servicios que invocan "funciones como un servicio" de aquellos que reciben "funciones como un servicio".

Si es necesario que el mismo recurso o servicio invoque y reciba una "función como un servicio" asegúrese de:
  
- Establecer una convención de nombres que ayude a identificar posibles ciclos.

- Configurar el límite de escalamiento de la función. No evita el bucle, pero limita los recursos consumidos.

- Crear alarmas para monitorear el escalamiento de una función y así, recibir alertas si el escalamiento aumenta repentinamente.
