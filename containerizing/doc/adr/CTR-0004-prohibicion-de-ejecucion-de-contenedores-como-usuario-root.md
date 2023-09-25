# ADR CTR 0004. Prohibición de ejecución de contenedores como usuario root

Date: 2023-09-04

## Keywords

containerizing, container, uso, contenedor, producción, ejecución, root, usuario. 

## Status

Accepted

## Context

Lanzar una aplicación contenerizada con privilegios de "root" es posible. Sin embargo, esta forma de ejecución permite a cualquier persona o cuenta, que tenga acceso al contenedor, obtener mayores privilegios de los que debería disponer y así, realizar acciones sobre los recursos que no le eran permitidas, vulnerando no solamente el contenedor sino posibilitando su escalamiento hacia otras partes del sistema.

## Decision

Configuramos los contenedores para que se ejecuten como "no root".

El principio de privilegio mínimo es un principio que establece que un usuario o cuenta debe poseer solo aquellos privilegios que son esenciales para realizar sus funciones. Al garantizar este principio, al momento de ejecutar el contenedor, ampliamos la seguridad, estableciendo que usuarios pueden ejecutar que procesos, a qué volúmenes y a qué puertos pueden acceder en el contenedor.

Las aplicaciones ejecutadas en contenedores como "no root" garantizan un entorno más seguro.

## Consequences

Requerimos especificar un usuario "no root" para la ejecución del contenedor. Esto es indicado mediante una directiva en el propio archivo que describe los pasos de construcción de la imagen del contenedor. 

Requerimos establecer permisos de acceso (lectura, escritura o ejecución) para el usuario especificado como "no root" sobre los archivos y los directorios que serán utilizados en la ejecución de la aplicación contenerizada.

El siguiente es un ejemplo de un servicio ejecutando como usuario "no root":

```
FROM node:16.17.0-bullseye-slim
RUN apt-get update && apt-get install -y --no-install-recommends dumb-init
...
WORKDIR /usr/src/app
#  Permisos de acceso al usuario "no root"
COPY --chown=1001:1001 . /usr/src/app
# Usuario "no root"
USER 1001   
CMD ["dumb-init", "node", "server.js"]
```

