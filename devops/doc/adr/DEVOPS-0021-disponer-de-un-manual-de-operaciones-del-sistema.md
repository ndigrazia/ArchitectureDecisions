# ADR DEVOPS 0021. Disponer de un manual de operaciones del sistema

## Keywords

devops, runbook, manual, mantenimiento, operaciones.

## Status

Accepted

## Context

¿Qué es lo que más molesta a un equipo de desarrollo o de operaciones? Seguramente tener que levantarse a las 3:00 de la mañana a resolver fallas ocurridas durante la ejecución de la aplicación. Contar con un manual de operaciones (o runbook) ayuda a evitar esas situaciones molestas.

## Decision

Confeccionaremos un manual de operaciones con información de soporte que permita al equipo de operaciones operar el sistema, principalmente en situaciones de fallas.

Este documento es creado por los desarrolladores y es mantenido por ambas partes. El equipo de operaciones contribuye en el documento con sus acciones realizadas.

Como mínimo un manual de operaciones debe incluir:

- Descripción general: ¿Por qué desarrollamos el sistema?.
  
- Contrato: ¿Cuál es el comportamiento esperado para el sistema? ¿Cómo se supone que otros sistemas interactúen con él? Acuerdos con otros sistemas que garantizan la durabilidad, confiabilidad o disponibilidad del servicio.
  
- Funcionalidad: ¿Cómo funciona el software?.
  
- Funcionalidad operativa: ¿Cómo funciona el sistema en el ambiente operativo? ¿Qué infraestructura lo soporta? ¿Cómo se despliega?.
  
- Observabilidad:  ¿Qué métricas permiten ver su estado y su rendimiento? ¿Qué alertas están indicadas? ¿Qué significa si alguna métrica escapa del valor esperado? ¿Cuáles son los límites de las métricas?. Especificación de los estados de fallas basados ​​en las métricas disponibles.

- Respuesta ante la falla: ¿Cuáles son las acciones comunes que un operador puede tomar para resolver un problema? ¿Qué acciones se deben tomar primero para comprender mejor y remediar la situación?. ¿Qué pasos puede tomar un operador para investigar el comportamiento, solucionar un problema o tratar de recuperar una falla completa?.

- Conocimiento no documentado: ¿Qué se necesita saber que no está en los documentos? ¿Por qué estamos usando eso?¿Por qué se tomó esa decisión en lugar de otra?.
  
## Consequences

El proceso de generación del documento agrega trabajo adicional al desarrollo del sistema. Sin embargo, puede iniciarse en las fases tempranas de diseño, lo que agiliza su proceso de construcción.

Mantiene el conocimiento de la operación del sistema centralizado en único documento.

Facilita la respuesta ante incidencias o fallas.
