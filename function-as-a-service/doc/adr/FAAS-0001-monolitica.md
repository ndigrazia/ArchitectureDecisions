# ADR FAAS 0001. Monolítica

## Keywords

faas, serverless, función, sin servidor, monolítico, servicio, monolítica.

## Status

Accepted

References [ADR FAAS 0020. Estrangulador](FAAS-0020-estrangulador.md)

References [ADR FAAS 0017. Servicio simple](FAAS-0017-servicio-simple.md)

## Context

Con frecuencia, durante la migración de aplicaciones tradicionales hacia nuevos modelos de desarrollo, muchos desarrolladores hacen uso de los componentes de software en su estado actual, sin aplicar las modificaciones necesarias que llevarían a alcanzar los beneficios ofrecidos por los nuevos paradigmas.

Dado que las "funciones como un servicio" (sin servidor) se están empleando con más frecuencia hoy en día, surge la inquietud de sí se debe utilizar una función que contenga toda la lógica de la aplicación (monolítica) o si se debe descomponer las funcionalidades de la aplicación en funciones individuales que tengan una única responsabilidad.

Entregar la lógica de un monolito como una "función como un servicio" simplemente evita la gestión de servidores, pero no posibilita obtener los beneficios de su uso. 

## Decision

No diseñaremos "funciones como servicio" que contengan toda la lógica que es ejecutada para todos los eventos que procese una aplicación. Es decir, que el ruteo de las funcionalidades de la aplicación sea realizado dentro de la propia aplicación.

Una "función como un servicio" monolítica es una función con toda la lógica de la aplicación con un API Gateway enfrente de esta. Puede ser un punto de entrada para comenzar a utilizar la tecnología pero no posibilita obtener los beneficios de su uso.

Con estrategias como el "patrón estrangulador", se puede migrar el código de la aplicación monolítica a servicios individuales.

Nuestro objetivo es que cada función realice solo una acción o tarea.

## Consequences

Requerimos descomponer toda la lógica de la aplicación en servicios individuales.
