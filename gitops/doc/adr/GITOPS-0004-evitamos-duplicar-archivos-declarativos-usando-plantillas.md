# ADR GITOPS 0004. Evitamos duplicar archivos declarativos usando plantillas

Date: 2024-03-07

## Keywords

gitops, devops, estado, deseado, declarativo, declarativa, plantilla.

## Status

Accepted

References [ADR GITOPS 0002. Estado deseado inmutable y versionado](GITOPS-0002-estado-deseado-inmutable-y-versionado.md)

References [ADR GITOPS 0001. Estado deseado del sistema expresado de forma declarativa](GITOPS-0001-estado-deseado-del-sistema-expresado-de-forma-declarativa.md)

## Context

En el contexto de GitOps, la idea principal es mantener la declaración del estado del sistema de forma declarativa en un espacio centralizado (repositorio). Esto implica por ejemplo, describir la configuración de los recursos en archivos YAML y almacenarlos en un repositorio Git. Sin embargo, para evitar la repetición excesiva de código YAML entre varios ambientes o clústeres, podemos seguir algunas prácticas y herramientas que facilitan la gestión de la configuración de manera eficiente. 

## Decision

Evitaremos duplicar los archivos declarativos mediante el uso de plantillas.

## Consequences

Evitar la duplicación de archivos declarativos en un contexto de GitOps asegura que la configuración sea coherente en todos los entornos, reduce el riesgo de errores, especialmente cuando se deben realizar cambios, permite el reuso de fragmentos de configuración en varios contextos, facilita a la colaboración entre equipos, ya que todos trabajan sobre una única fuente de verdad, ayuda en la revisión y la auditoría de los cambios.

Emplearemos algunas de las siguientes estrategias para evitar la redundancia de archivos declarativos:

- Uso de Helm Charts: Helm es un administrador de paquetes que utiliza "charts" para describir aplicaciones. Los charts son paquetes preconfigurados (plantillas), almacenados en un repositorio. Helm puede injectar valores en los parámetros definidos en las plantillas, reduciendo la redundancia de los archivos declarativos (YAMLs).

- Uso de Kustomize: Kustomize es una herramienta de personalización que permite gestionar la configuración de los recursos utilizando capas (bases) y parches (overlays). Puede dividir la configuración en capas y aplicar parches específicos según el entorno o requisitos. Esto ayuda a evitar la duplicación de código.


