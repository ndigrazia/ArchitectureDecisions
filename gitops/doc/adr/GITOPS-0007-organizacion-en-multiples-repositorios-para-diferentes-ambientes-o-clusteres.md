# ADR GITOPS 0007. Organización en múltiples repositorios para diferentes ambientes o clústeres

Date: 2024-03-08

## Keywords

gitops, devops, estado, configuración, declarativa, repositorio, múltiple, organización.

## Status

Accepted

Referenced by [ADR GITOPS 0009. Entornos de configuración separados en directorios no en ramas](GITOPS-0009-entornos-de-configuracion-separados-en-directorios-no-en-ramas.md)

## Context

La organización de repositorios de código fuente es un aspecto crítico en el desarrollo de software, y existen varias estrategias para gestionar la estructura y la distribución de los repositorios. Dos enfoques comunes son el uso de "monorepos" y "polirepos".

Un monorepo (Único Repositorio) almacena todo el código fuente de las aplicaciones, de las configuraciones de los clústeres y de las configuraciones de los ambientes en un solo repositorio de control de versiones.

Polirepos (Múltiples Repositorios) almacena el código fuente, las configuraciones de clúster y las configuraciones de ambientes en repositorios independientes. 

## Decision

Emplearemos Polirepos para almacenar la información de configuración necesaria de los entornos y clusteres.  

## Consequences

Las ventajas asociadas con el uso de un enfoque de polyrepo son:

- Se puede dividir un proyecto en módulos más pequeños y gestionarlos de forma independiente. 

- Es mas flexible y escalable, ya que puede hacer que sea más fácil gestionar el crecimiento de los proyectos al permitir  que equipos diferentes trabajen en diferentes partes de la configuración del sistema.

- Los proyectos pueden utilizar diferentes herramientas y flujos de trabajo.

No obstante, el enfoque presenta las desventajas siguientes:

- Incremento de la complejidad debido a la cantidad de repositorios resultantes.

- Riesgos de conflictos con librerias compartidas entre diferentes proyectos almacenados en repositorios individuales.

Para implementar un enfoque polyrepo necesitamos tener presente las siguientes consideraciones:

- Asegurar que el "Sistema de Control de Versiones" puede escalar según las necesidades y el número de equipos de trabajo.

- Establecer claramente los limites entre los repositorios. Generalmente, las separaciones pueden realizarse en función de los intereses de los departamentos de una organización.

- Acordar politicas de compartición de librerias, estableciendo como se realizará su uso entre los diferentes proyectos almacenados en diferentes repositorios.

- Usar un gestor para administrar las dependencias entre los proyectos.

- Emplear flujo de trabajos automaticos (pipelines) para automatizar el proceso de construcción y despliegue de los cambios.

- Usar contenedores para la entrega de valor.

Si tenemos en cuenta las anteriores consideraciones a la hora de implementar el enfoque polyrepo, consideramos que los beneficios superan sus desafíos.

