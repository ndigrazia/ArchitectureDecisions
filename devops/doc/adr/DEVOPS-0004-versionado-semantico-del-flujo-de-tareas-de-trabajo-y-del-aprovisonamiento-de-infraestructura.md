# ADR DEVOPS 0004. Versionado semántico del flujo de tareas de trabajo y del aprovisionamiento de infraestructura

Date: 2022-12-19

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, etapas, versionado, semántico, aprovisionamiento.

## Status

Accepted

Referenced by [ADR DEVOPS 0002. Declaración como código del flujo de trabajo usado en el desarrollo y el mantenimiento de las aplicaciones en la nube](DEVOPS-0002-declaracion-como-codigo-del-flujo-de-trabajo-usado-en-el-desarrollo-y-mantenimiento-de-las-aplicaciones-en-la-nube.md)

Referenced by [ADR DEVOPS 0006. Aprovisionamiento como código de los recursos de la infraestructura IT](DEVOPS-0006-aprovisionamiento-como-codigo-de-los-recursos-de-la-infraestructura-it.md)

## Context

Las actividades de control de versiones nos posibilitan identificar, controlar y getionar el cambio en los componentes de software a lo largo de su ciclo de vida, permitiendo conocer el estado en el que se encuentran cada uno de los componentes en un momento dado de su desarrollo e, identificar cual es el significado y la naturaleza del cambio realizado.

Como parte de las actividades de control de versiones es sumamente importante definir e interpretar el esquema a usar para el control de versiones. Esta definición y entendimiento les permitirá a los desarrolladores poder comunicar los cambios incluidos en una versión del proyecto o servicio.

## Decision

Usaremos el versionado semántico para el versionado de los archivo de código que declaren el flujo de tareas de trabajo y el aprovisionamiento de la infraestructura.

Esta estrategia nos permite establecer cual es el significado que implementa una u otra versión mediante tres partes: cambios incompatibles,cambios compatibles y parches.

## Consequences

El versionado semántico permite realizar un seguimiento de todos los cambios y la evolución de los flujos de trabajo y de los recursos que implementan una infraestructura IT.

Un mal entendimiento del esquema de versionado semántico no permitirá señalar adecuadamente los cambios y como consecuencia, cambios importantes pueden no ser liberados o llevar a una liberación de cambios en un momento inadecuado. Esto último es bastante fácil de mitigar con el aprendizaje y la utilización de herramientas de automatización.
