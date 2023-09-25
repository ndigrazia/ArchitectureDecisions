# ADR FAAS 0011. Autenticación de usuarios

Date: 2023-03-13

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, autenticación, caso uso.

## Status

Accepted

References [ADR FAAS 0008. Patrones de carga predecibles](FAAS-0008-patrones-de-carga-predecibles.md)

## Context

Los principales proveedores de la nube ofrecen servicios para gestionar y para validar la identidad de los usuarios mediante servicios de Gestión de Identidad y Acceso (IAM). Las sesiones otorgadas por estos servicios aseguran los privilegios de acceso a otros servicios gestionados por el propio proveedor de la nube. Por ejemplo, servicio de almacenamiento de archivos o de entrega de mensajes.

El empleo de los mecanismos de identidad ofrecidos por el proveedor de la nube ayudan a simplificar nuestra solución al reducir la cantidad de servidores y al permitir enfocarse en escribir solo la lógica de negocio sin necesidad de anexar lógica de infraestructura.
 
Si bien, los servicios de identidad en la nube ofrecen muchas ventajas, pueden limitar las opciones de validación de entrada de los usuarios. 

En caso de requerir validaciones personalizadas, es posible el empleo de funciones o contenedores dependiendo de la previsibilidad de su carga o la frecuencia de su uso.

## Decision

Usaremos una "función como un servicio" para validaciones de identidad personalizadas de uso poco frecuentes o impredecibles.

La "función como un servicio" puede realizar las validaciones de identidad personalizadas y apoyarse en los mecanismos de identidad ofrecidos por el proveedor de la nube para facilitar la comunicación con otros servicios administrados por el propio proveedor.

Conectamos la "función como un servicio" detrás de un API Gateway para procesar las validaciones personalizadas. Luego, retornamos al API Gateway la política de acceso (los permisos otorgados), los cuales se apoyan en el mecanismo brindado por el proveedor para el control de acceso. Por ejemplo, en el caso de la nube de AWS la función retorna un IAM policy. Finalmente, el API Gateway usa esa política para validad la solicitud, ruteando o rechazando la misma.

## Consequences

Requerimos el empleo de un API Gateway en donde las peticiones serán dirigidas para evaluaciones de seguridad.

Requerimos una plataforma de ejecución de la solución sin servidor.

Requerimos una solución de autenticación personalizada con alta performance y alta disponibilidad.
