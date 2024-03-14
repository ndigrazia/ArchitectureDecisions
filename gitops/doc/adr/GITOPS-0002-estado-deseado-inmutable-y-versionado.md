# ADR GITOPS 0002. Estado deseado inmutable y versionado

Date: 2024-03-06

## Keywords

gitops, devops, estado, deseado, declarativo, declarativa, inmutable, versionado.

## Status

Accepted

References [ADR GITOPS 0001. Estado deseado del sistema expresado de forma declarativa](GITOPS-0001-estado-deseado-del-sistema-expresado-de-forma-declarativa.md)

Referenced by [ADR GITOPS 0003. estado del sistema continuamente reconciliado](GITOPS-0003-estado-del-sistema-continuamente-reconciliado.md)

Referenced by [ADR GITOPS 0004. Evitamos duplicar archivos declarativos usando plantillas](GITOPS-0004-evitamos-duplicar-archivos-declarativos-usando-plantillas.md)

## Context

Mantener un registro claro y seguro de los cambios realizados sobre el estado de un sistema es esencial para diversos propósitos, como la auditoría, la solución de problemas, la reversión de cambios no deseados y la colaboración entre equipos. Para lograr esto, se suelen utilizar prácticas específicas.

## Decision

Almacenaremos el estado deseado asegurando su inmutabilidad y su versionado.

Utilizaremos un sistema de control de versiones para registrar y gestionar cambios en las declaraciones del estado del sistema. 

Los conceptos de "versionado" e "inmutabilidad" están estrechamente relacionados en el ámbito de la gestión y manipulación de datos, especialmente en el desarrollo de software y la administración de sistemas. Ambos conceptos se utilizan para mantener un registro claro y seguro de los cambios realizados en un sistema y garantizar la integridad de los datos a lo largo del tiempo.  

Finalmente, en lugar de modificar registros existentes, crearemos nuevos registros para representar el estado actual.

## Consequences

Cada "commit" representa una instantánea del sistema en un punto específico del tiempo. 

El repositorio que contiene la configuración declarativa del sistema se le conoce con el nombre de "fuente de verdad".

Al emplear un sistema de control de versiones podemos mantener registros detallados de los cambios realizados, documentando qué se modificó, quién lo hizo y cuándo.

