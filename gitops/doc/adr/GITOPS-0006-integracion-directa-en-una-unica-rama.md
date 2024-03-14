# ADR GITOPS 0006. Integración directa en una única rama

Date: 2024-03-07

## Keywords

gitops, devops, estado, configuración, declarativa, repositorio.

## Status

Accepted

## Context

Existen varios enfoques para gestionar el desarrollo de software utilizando sistemas de control de versiones (SCV). Estos enfoques varían en la forma en que se estructuran las ramas, se manejan las integraciones y se gestionan las versiones. "Trunk-Based Development" y "GitFlow" son algunos de estos enfoques. La estrategia "Trunk-Based Development" utiliza principalmente una rama principal (trunk o main) para el desarrollo mientras, en "GitFlow" se emplean múltiples tipos de ramas, como ramas de características, de desarrollo, de liberación y de mantenimiento.

## Decision

Emplearemos el enfoque de rama única o "Trunk-Based Development" para gestionar los cambios en las configuraciones en la metodología GitOps.

En este enfoque se define una única rama principal, gestionando cada cambio de configuración en una rama diferente de corta duración (rama temporal). Cuando se finaliza el cambio, el desarrollador crea una solicitud (Pull Request/Merge Request) para liberar su modificación hacia la rama principal. Finalmente, se elimina la rama temporal.

## Consequences

Emplear una única rama principal favorece la "entrega continua" al permitir la integración de cambios directamente en la rama principal, reduce la posibilidad de conflictos y problemas de integración, al realizar integraciones frecuentes en la rama principal, facilita la detección temprana de errores, fomenta una mayor colaboración entre los miembros del equipo.

No obstante, el enfoque de única rama principal requiere una madurez significativa en prácticas de desarrollo ágil, pruebas automatizadas y colaboración efectiva. Equipos menos maduros pueden enfrentar desafíos al adoptar este enfoque.  

Pasos a seguir para implementar "Trunk-Based Development":

1. Establecer la "rama principal".
2. Crear una "rama temporal" para aplicar los cambios de configuración.
3. Generar una solicitud de cambio (Pull Request/Merge Request) hacia la "rama principal".
4. Revisar y aprobar la modificación.
5. Eliminar la "rama temporal".

