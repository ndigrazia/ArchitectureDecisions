# ADR FAAS 0005. Llamadas a componentes sin capacidad de escalamiento

Date: 2023-03-03

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, escalamiento, capacidad.

## Status

Accepted

## Context

Los usuarios de una aplicación son sus puntos impredecibles, ya que probablemente harán, en algún momento, una oleada de invocaciones que pueden provocar un colapso del sistema.

Las características de escalamiento de la tecnología de "función como un servicio" permiten tratar el aumento repentino de la carga, pero los servicios que no soporten el escalamiento instantáneo o el manejo de solicitudes masivas, no permitirán manipular ese aumento de carga, generando el colapso del sistema.

La tecnología de "función como un servicio" colapsará los servicios usados por ella que no permitan adaptarse al aumento de la carga.

## Decision

No diseñaremos funciones que usen directamente servicios o recursos que no permitan adaptarse automáticamente al aumento de la carga.

## Consequences

Mediremos la capacidad de escalamiento de los recursos o servicios usados en la "función como un servicio" para asegurarnos que pueden adaptarse al aumento de la carga manejado por dicha función.

Usaremos una arquitectura asincrónica basada en colas para las invocaciones de funciones a servicios o recursos que no pueda adaptarse al aumento de carga.

Configuraremos el límite de escalamiento de la función para limitar los recursos consumidos.

En caso de contar con servicios que puedan escalar, pero no puedan hacerlos automáticamente podemos usar funciones para realizar dicho escalamiento, identificando los eventos que permitan dispararlas.
