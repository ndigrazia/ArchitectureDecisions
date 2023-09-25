# ADR FAAS 0027. Cifrado de los secretos y su almacenamiento en variables de contexto

Date: 2023-04-17

## Keywords

faas, serverless, función, sin servidor, servicio, cifrado, secreto, recurso, clave, key, kms.

## Status

Accepted

## Context

No es seguro proporcionar junto a la "función como un servicio" los secretos en forma plana, ya que si bien son usados para realizar su trabajo y le otorgan acceso a los recursos de producción, abren a la posibilidad de que cualquier observador pueda acceder sobre ellos. Generalmente, los proveedores de la nube brindan servicios, como por ejemplo Key Management Service (KMS), que permiten proteger sus secretos y las integraciones con otros servicios de la propia nube.

Con el objetivo de proteger los secretos, se deben cifrar los mismos mediante los mecanismos de seguridad provistos por la plataforma y almacenar su versión cifrada de tal manera que, sea la propia "función como un servicio", la única en conocer como acceder a los recursos que la misma requiere.

## Decision

Usaremos el Servicio de Administración de Claves (KMS) de la plataforma para proteger los secretos. Este servicio generará y almacenará las claves de cifrado.

Nunca accederemos de manera directa a las claves administradas por el Servicio de Administración de Claves.

Encriptamos los secretos y almacenamos su versión cifrada en las variables de entorno de la "función como un servicio".

## Consequences

Requerimos una plataforma de ejecución de la solución sin servidor.

Requerimos conocer y entender el Servicio de Administración de Claves ofrecido por el proveedor en la nube.

Necesitamos que el código de la función (fuera del controlador de función) detecte los valores cifrados y los descifre antes de utilizar los secretos.

Solicitamos otorgar privilegios a la función para utilizar el Servicio de Administración de Claves.

El uso de mecanismos de cifrado de los secretos puede afectar el tiempo de respuesta de la  "función como un servicio". Principalmente, al momento de su inicialización.

