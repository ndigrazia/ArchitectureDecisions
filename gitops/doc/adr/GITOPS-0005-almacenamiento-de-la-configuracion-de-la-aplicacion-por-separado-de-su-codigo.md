# ADR GITOPS 0005. Almacenamiento de la configuración de la aplicación por separado de su código

Date: 2024-03-07

## Keywords

gitops, devops, estado, configuración, declarativa.

## Status

Accepted

Referenced by [ADR GITOPS 0008. Método de despliegue activado por CI y adueñado por GitOps](GITOPS-0008-metodo-de-despliegue-activado-por-ci-y-adueñado-por-gitops.md)

## Context

Se presentan dos formas de almacenar la configuración de la aplicación. Por un lado, almacenar la configuración de la aplicación junto a su código (mismo repositorio) y por el otro, separar el código de la aplicación de su configuración (diferentes repositorios).

Almacenar en conjunto la configuración de la aplicación y su código es una práctica especialmente deseada cuando se quiere tener una configuración específica vinculada a una versión específica del código. 

## Decision

Separaremos el código de la aplicación de su configuración.

La separación entre el código de la aplicación y sus configuraciones es una buena práctica en desarrollo de software y gestión de infraestructura. Esta práctica facilita la gestión, mantenimiento y escalabilidad del sistema. 

## Consequences

Creamos diferentes repositorios para almacenar por separado la configuración y el código de la aplicación.

Al separar el código de la configuración de la aplicación se logra:

- Evitar la reconstrucción de la aplicación si su configuración cambia pero no su código.

- Garantizar ciclos independientes de construcción y configuración.

- Definir perfiles o entornos específicos que contengan configuraciones adaptadas a esos contextos (desarrollo, prueba, producción).

Por otro lado, puede presentar algunas desventajas como el aumento del tiempo dedicado a la gestión de los flujos de construcción y configuración. Sin embargo, consideramos que los beneficios superan sus desafíos.

