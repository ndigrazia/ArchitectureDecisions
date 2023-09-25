# ADR DEVOPS 0006. Aprovisionamiento como código de los recursos de la infraestructura IT

Date: 2022-12-22

## Keywords

devops, aprovisionamiento, entrega, despliegue, recurso, código, declarativo.

## Status

Accepted

References [ADR DEVOPS 0004. Versionado semántico del flujo de tareas de trabajo y del aprovisionamiento de infraestructura](DEVOPS-0004-versionado-semantico-del-flujo-de-tareas-de-trabajo-y-del-aprovisonamiento-de-infraestructura.md)

## Context

En el pasado, el equipo de operaciones tenía que administrar y configurar manualmente todo el hardware y software requerido para el funcionamiento de las aplicaciones. En los últimos años, la tecnología en la nube cambió la forma que las organizaciones piensan, desarrollan y mantienen su infraestructura de IT.

La Infraestructura como Código (IaC) se volvió una práctica crítica de la tendencia en la nube permitiendo declarar y aprovisionar la infraestructura de IT mediante archivos.

## Decision

Implementaremos el aprovisionamiento recursos de infraestructura IT mediante un enfoque declarativo dentro de archivos de código.

El equipo debe definir los recursos de la infraestructura de IT (redes, discos, máquinas, sistemas operativos, etc.) en archivo de código versionable y almacenado en un repositorio de fuentes.

Un enfoque declarativo de las tareas hace uso de un lenguaje específico de dominio con estructuras y bloques bien formados.

Se usa un repositorio de fuentes como la fuente confiable de la información de la infraestructura. Cualquier modificación en dicha información resultará en cambios automáticos en su infraestructura asociada.

Esta práctica constituye la base del patrón de Infraestructura como Código.

## Consequences

El enfoque declarativo de la infraestructura disminuye costos, reduce riesgos, mejora los tiempos de despliegue y facilita su entendimiento, volviendo comprobable, repetible y testeable la infraestructura.

El empleo de esta práctica requiere considerar ciertos aspectos: 

- Empleo y entendimiento de una herramienta de aprovisionamiento de infraestructura.

- Empleo de una herramienta de versionado de código.

- Definición de la estrategia usada en el control de cambios en las fuentes.

- Entendimiento del lenguaje específico de dominio usado para aprovisionar recursos de la infraestructura.
