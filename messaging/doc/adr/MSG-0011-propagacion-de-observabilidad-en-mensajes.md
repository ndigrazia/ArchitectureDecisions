# ADR MSG 0011. Propagación de observabilidad en mensajes

## Keywords

messaging, message, asincrónica, mensaje, cola, observabilidad

## Status

Accepted

## Context

Es necesario disponer una traza punta a punta de las distintas transaciones que se ejecuten en los sistemas. Los mensajes deben dar continuidad a la traza para lograr esta observabilidad.

## Decision

Utilizaremos la meta información del mensaje para transportar este tipo de información.

## Consequences

Desarrollar los componentes reutilizables (librería o sidecar) responsables de este manejo.
