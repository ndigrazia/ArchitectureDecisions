# ADR DEVOPS 0002. Declaración como código del flujo de trabajo usado en el desarrollo y el mantenimiento de las aplicaciones en la nube

Date: 2022-12-16

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, código, declarativo.

## Status

Accepted

References [ADR DEVOPS 0004. Versionado semántico del flujo de tareas de trabajo y del aprovisionamiento de infraestructura](DEVOPS-0004-versionado-semantico-del-flujo-de-tareas-de-trabajo-y-del-aprovisonamiento-de-infraestructura.md)

## Context

Los servicios en la nube han impactado en la forma como las empresas construyen sus aplicaciones, reemplazando el desarrollo de aplicaciones monolíticas por aplicaciones basadas en servicios distribuidos, escalables e individuales. La gran cantidad y diversidad de servicios, que pueden llegar a componer a aplicaciones complejas, hace que sea fácil cometer errores durante los procesos de construcción y aprovisionamiento.

Las prácticas del pasado se orientaron a la realización del flujo de trabajo mediante un proceso manual, en el cual se solicitaban las tareas de implementación, que el equipo de operaciones debía realizar, mediante formularios web o documentos formales.  

El desarrollo de aplicaciones modernas requiere de un enfoque diferente que permita evitar errores en la construcción y aprovisionamiento de los servicios de las aplicaciones en la nube. Los procesos automatizados y la declaración del flujo de trabajo como código constituyen las prácticas sobre las cuales se sustenta la provisión de servicios de la nube.

## Decision

Implementaremos flujos de trabajo automáticos mediante un enfoque declarativo de las tareas a realizar dentro de archivos de código.

El equipo debe definir las tareas del flujo de trabajo (compilación, prueba, despliegue, etc.) en archivo de código versionable y almacenado en un repositorio de fuentes.

La declaración del trabajo en un archivo versionado permite que los cambios se puedan trazar, probar y corregir.

Un enfoque declarativo de las tareas hace uso de un lenguaje especifico de dominio con estructuras y bloques bien formados.

Esta práctica, conocida como Pipeline as Code (PaC), permite administrar, controlar y ejecutar flujos de trabajo consistentes y repetibles sin la necesidad de realizar procesos manuales.

Se usa un repositorio de fuentes como una fuente confiable del flujo de trabajo.

## Consequences

La declaración de flujos de trabajo como código tiene varios beneficios:

- Velocidad: El flujo de trabajo se puede modificar rápidamente, ayudando a la entrega apropiada del servicio.

- Eficacia: Se estandariza el proceso de trabajo reduciendo los errores humanos.

- Gestión de riesgos: Debido al control de versiones, cada cambio puede ser documentado, registrado, rastreado y probado.

El empleo de esta práctica requiere considerar ciertos aspectos: 

- Empleo de una herramienta de versionado de código.

- Definición de la estrategia usada en el control de cambios en las fuentes.

- Entendimiento del lenguaje específico de dominio usado en la definición de las tareas del flujo de trabajo.

- El lenguaje específico de dominio proporciona una sintaxis más restrictiva.

- Entendimiento del software usado para la implementación del flujo continuo.
