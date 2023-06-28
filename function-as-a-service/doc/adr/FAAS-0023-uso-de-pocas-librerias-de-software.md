# ADR FAAS 0023. Uso de pocas librerías (o bibliotecas) de software

## Keywords

faas, serverless, función, sin servidor, servicio, concurrencia, escalamiento, librería, biblioteca.

## Status

Accepted

## Context

Una de las debilidades de la solución de "función como un servicio" es el inicio en frío, el cual ocurre cuando se produce la invocación a una función y no existe ninguna instancia disponible para realizar el tratamiento de la petición. En este escenario un nuevo contenedor (posiblemente también una instancia de máquina virtual) tiene que ser iniciado, provocando, como consecuencia, una demora en la resolución del pedido.

Además, del tiempo requerido para iniciar el contenedor, el cual puede verse incrementado por el inicio de una máquina virtual y su adición al cluster (dependiendo del número de solicitudes concurrentes), tenemos el tiempo de latencia de puesta en marcha de la función misma, el cual está muy relacionados con su forma de desarrollo y con la cantidad de librerías o bibliotecas usadas.

## Decision

Usaremos la menor cantidad posible de bibliotecas o librerías en la implementación una "función como un servicio".

Emplear demasiadas librerías demora el inicio de las funciones.

Si latencia de respuesta es un factor decisivo en la aplicación, entonces es posible que una "función como un servicio" no sea la más adecuada para su caso de uso.

## Consequences

Requerimos una plataforma de ejecución de la solución sin servidor.

Usaremos lenguajes de desarrollo con una huella de memoria pequeña.

Usaremos librerías o bibliotecas desarrolladas que siguen prácticas ingenieriles y que tengan cierta madurez.

Usar pocas librerías permite mejorar el periodo de inicio de las funciones, el cual hace más fácil su escalamiento y disminuye el tiempo de su respuesta.
