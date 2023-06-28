# ADR FAAS 0015. Procesamiento de archivos o imágenes

## Keywords

faas, serverless, función, sin servidor, servicio, tarea, procesamiento, archivo, imagen, caso uso.

## Status

Accepted

## Context

Un posible caso de uso de una aplicación es el procesamiento de archivos o imágenes.

El procesamiento de archivos o imágenes consiste en subir el archivo o la imagen a un repositorio, su análisis y su gestión, el cual consiste en realizar ciertas tareas para obtener una imagen mejorada o extraer alguna información util. Finalmente, el resultado es almacenado en un repositorio de almacenamiento que generalmente es distinto del repositorio fuente.

Podemos realizar el tratamiento de archivos o imágenes con funciones o con contenedores.

## Decision

Usaremos una "función como un servicio" para realizar el procesamiento de archivos o imágenes.

Usaremos funciones para implementar este caso de uso debido a sus características periódicas, ya que el uso de contenedores involucraría el pago por sus horas de disponibilidad independientemente de su uso.

Al emplear una solución sin servidor podemos hacer uso de eventos dado que es una de las capacidades naturales de esta tecnología. Es decir, iniciaremos el tratamiento de archivos o imágenes una vez finalizadas sus cargas en el repositorio. Situación que es indicada por medio de un evento desencadenado por el propio receptor de dichos objetos, evitando tener que realizar periódicamente sondeos (polling) al repositorio fuente.

## Consequences

Requerimos el uso de repositorios de almacenamiento con capacidades de generación de eventos.

Requerimos una plataforma de ejecución de la solución sin servidor.

Requerimos lógica de procesamiento con alta performance y alta disponibilidad. Recordemos que una "función como un servicio" no es adecuada para tareas que llevan demasiado tiempo de ejecución o son demasiado complejas. 
