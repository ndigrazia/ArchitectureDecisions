# ADR FAAS 0010. Webhook entrantes

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, webhook, tercero, caso uso.

## Status

Accepted

References [ADR MSG 0003. Eliminación de mensajes basura encolados](../../../messaging/doc/adr/MSG-0003-eliminacion-de-mensajes-basura-encolados.md)

References [ADR FAAS 0008. Patrones de carga predecibles](FAAS-0008-patrones-de-carga-predecibles.md)

## Context

El proceso de integración tiene como objetivo combinar diferentes componentes software o sistemas más pequeños de manera tal que las responsabilidades y los datos contenidos en cada uno de ellos se convierten en parte de un sistema más grande.

Existen diferentes formas de integrar sistemas, mediante intercambio de archivos, invocación de APIs, invocación de servicios webs, etc. Cada una con sus ventajas y sus desventajas.

Dentro de las integraciones mediante APIs aparece una técnica llamada webhook que permite a los sistemas compartir información en tiempo real. 

Un webhook es una práctica usada para notificar cambios de estado o eventos específicos en una aplicación, haciendo que el interesado de esos cambios no tenga que estar comprobando periódicamente si dichos cambios ocurrieron o no. Por ejemplo, nuestro sistema podría recibir una notificación cuando una orden de pedido fuera creada, si previamente, hemos registrado que un webhook sea lanzado para ese evento en la aplicación. 

Estas peticiones pueden ser tratadas con funciones o con contenedores dependiendo de la previsibilidad de su carga o la frecuencia de su uso.

## Decision

Usaremos una "función como un servicio" para manipular eventos notificados mediante webhook que tienen patrones de uso poco frecuentes o impredecibles.

No invocaremos directamente a una "función como un servicio" como respuesta a una solicitud proveniente de un webhook de un tercero.

Una "función como un servicio" se adapta mejor a situaciones en donde las cargas no son predecibles (escalamiento impredecible para cumplir la demanda) y cuando su uso no es muy frecuente.

No responderemos directamente con una "función como un servicio" que contenga la lógica de tratamiento de la solicitud enviada. En su lugar, publicaremos en una ruta de API Gateway un punto de entrada a una función que retorne el código de respuesta adecuado, almacenando las solicitudes, a medida que se reciban, en una cola de mensajería. Luego, como respuesta a los mensajes almacenados, invocaremos a la función que contiene la lógica de procesamiento.

Requerimos el almacenamiento y el procesamiento de los mensajes fallidos. Esta acción puede ser realizada mediante una "función como un servicio".

## Consequences

Requerimos el uso de un bróker de mensajería (message broker) y colas de mensajería funcionando en alta disponibilidad.

Requerimos el empleo de un API Gateway en donde los eventos serán dirigidos y sometidos a evaluaciones de seguridad.

Requerimos una plataforma de ejecución de la solución sin servidor.
