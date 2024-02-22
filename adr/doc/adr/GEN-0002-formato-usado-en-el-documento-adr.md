# ADR GEN 0002. Formato usado en el documento ADR

Date: 2023-05-10

## Keywords

adr, log, decisión, registro, documento, formato.

## Status

Accepted

Referenced by [ADR GEN 0001. Uso de ADR para registro de decisiones de arquitectura](GEN-0001-uso-de-adr-para-registro-de-decisiones-de-arquitectura.md)

Referenced by [ADR GEN 0003. Proceso de adopción de un documento ADR](GEN-0003-proceso-de-adopcion-de-un-documento-adr.md)

Referenced by [ADR GEN 0004. Proceso de revisión de un documento ADR](GEN-0004-proceso-de-revision-de-un-documento-adr.md)

Referenced by [ADR GEN 0005. Proceso de obsolescencia de un documento ADR](GEN-0005-proceso-de-obsolescencia-de-un-documento-adr.md)

## Context
 
La elección del formato para el registro de las Decisiones de Arquitectura (ADR) es esencial para garantizar la consistencia y la comprensión clara a lo largo del tiempo. 

## Decision

Escribiremos cada documento ADR con las siguientes secciones:

**ADR <CONTEXTO\> XXXX. <TITULO\>**

**Date**: Fecha en que se tomó la decisión. El formato debería ser: YYYY-MM-DD.

**Keywords**: Términos o frases que representan las ideas o temas principales dentro del documento.

**Status**: Estado actual de la decisión. Los estados son: Proposed, Accepted, Superseded, Supersedes, Rejected y Disused.

**References**: La sección de referencias puede contener enlaces directos a otros ADRs relevantes, permitiendo que los lectores accedan fácilmente a decisiones anteriores que están vinculadas o que han influido en la decisión actual. 

**Context**: Breve descripción del contexto en el que se tomó la decisión. Incluye desafíos, requisitos o problemas específicos que influyeron en la elección.

**Decision**: Estableceremos la decisión de la arquitectura y proporcionaremos una justificación detallada de la decisión.

**Consequences**: Describiremos las consecuencias después de que se tome la decisión y también, discutimos las ventajas y desventajas que se consideraron. Incluye impactos en el rendimiento, mantenimiento, escalabilidad, etc.

**Notes**: Identificación de las personas o equipos responsables de implementar y dar seguimiento a la decisión.

Este formato proporciona un marco estructurado para registrar decisiones de Arquitectura de manera consistente. La numeración secuencial (XXXX) facilita la organización y referencia, mientras que las secciones como Contexto, Decisión y Consecuencias, aseguran que se capture la información crucial.

## Consequences

Si el equipo de Arquitectura abandona el uso del formato establecido pierde simplificación en la creación de documentos de arquitectura, disminuye la lecto comprensión de sus decisiones y desaprovecha el uso de las herramientas que emplean dicho formato y permiten aliviar su carga de trabajo. 



