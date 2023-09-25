# ADR DEVOPS 0010. Uso de repositorio de imágenes para almacenamiento de imágenes doradas

Date: 2022-12-27

## Keywords

devops, repositorio, entrega, despliegue, flujo, imagen, inmutable, dorada.

## Status

Accepted

Referenced by [ADR DEVOPS 0009. Versionado semántico de las imágenes doradas](DEVOPS-0009-versionado-semantico-de-las-imagenes-doradas.md)

Referenced by [ADR DEVOPS 0013. Escaneo de vulnerabilidades en imágenes doradas](DEVOPS-0013-escaneo-de-vulnerabilidades-en-imagenes-doradas.md)

## Context

El empleo de imágenes doradas (golden image), como alternativa a los procesos manuales, permiten ahorrar tiempo y garantizar la consistencia en el aprovisionamiento y la configuración del software, al eliminar la necesidad de cambios de configuración repetitivos sobre la misma infraestructura.

Con el uso de imágenes doradas aparece la necesidad de almacenarlas y de distribuirlas en diversos ambientes.

Los repositorios de imágenes permiten almacenar y proteger la imágenes con políticas y control de acceso basado en roles, garantizando que sean confiables, mediante la ejecución de análisis de vulnerabilidades. Además, actúan como punto de distribución, permitiendo la carga y la descarga de las imágenes en otros entornos.

## Decision

Emplearemos repositorios de imágenes para almacenamiento de imágenes doradas.

El proceso de generación de una imagen dorada implica un flujo de trabajo de integración continua y entrega continua. Concluidas las fases de construcción, la imagen resultante es almacenada en un repositorio de imágenes desde donde, se reúsa en diversos entornos de la organización.

## Consequences

Los repositorios de imágenes permiten almacenar y distribuir las imágenes en diversas partes del sistema, obtener información sobre las vulnerabilidades o los problemas existentes en las imágenes, auditoria de su uso y colaboración entre los desarrolladores.

Sin embargo, también requieren de la comprensión y el entendimiento de la herramienta usada para el almacenamiento de imágenes.
