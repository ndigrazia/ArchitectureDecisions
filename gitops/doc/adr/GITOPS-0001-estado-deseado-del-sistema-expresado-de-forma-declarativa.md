# ADR GITOPS 0001. Estado deseado del sistema expresado de forma declarativa

Date: 2024-03-06

## Keywords

gitops, devops, estado, deseado, declarativo, declarativa.

## Status

Accepted

Referenced by [ADR GITOPS 0002. Estado deseado inmutable y versionado](GITOPS-0002-estado-deseado-inmutable-y-versionado.md)

Referenced by [ADR GITOPS 0003. estado del sistema continuamente reconciliado](GITOPS-0003-estado-del-sistema-continuamente-reconciliado.md)

Referenced by [ADR GITOPS 0004. Evitamos duplicar archivos declarativos usando plantillas](GITOPS-0004-evitamos-duplicar-archivos-declarativos-usando-plantillas.md)

## Context

Un sistema es uno o más entornos compuestos de recursos, los cuales son administrados para su aprovisionamiento, su ejecución y su control de acceso. 

El concepto de "estado deseado" se refiere a la configuración para la provisión, la ejecución y la gestión de acceso que se espera lograr o mantener en un sistema en un momento específico. Existen dos enfoques para lograr el "estado deseado": El estado declarativo, el cual se centra en qué se quiere lograr sin especificar cómo y, el estado imperativo, el cual busca proporcionar instrucciones detalladas sobre cómo lograr un resultado específico.

## Decision

Expresaremos declarativamente el estado deseado del sistema. 

Nos centraremos en definir el resultado deseado o el estado final del sistema sin preocuparnos por los pasos específicos para alcanzar dicho estado.

## Consequences

El definir el estado del sistema en forma declarativa nos permite abstraer los detalles de implementación, lo que facilita su comprensión y su mantenimiento, ya que se enfoca en el resultado final sin detalles innecesarios. Finalmente, el código declarativo puede ser más propenso al paralelismo, ya que la ejecución de diferentes partes del código no depende estrechamente entre sí.

Como contrapartida, se pierde la definición explícita de los pasos que deben seguirse para lograr el resultado deseado.

Finalmente, almacenaremos las declaraciones en cualquier formato, usualmente nos enfocaremos en arhivos YAML.

