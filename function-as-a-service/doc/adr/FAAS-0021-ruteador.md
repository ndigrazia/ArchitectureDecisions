# ADR FAAS 0021. Ruteador

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, asincrónica, patrón.

## Status

Accepted

Referenced by [ADR FAAS 0002. Orquestador](FAAS-0002-orquestador.md)

## Context

En algunos casos de uso puede ser costoso el empleo de herramientas o servicios orientados a ejecutar complejos flujos de trabajo. Cuando la coordinación de actividades es simple podemos gestionarla usando un componente (Router) que actúe de moderador de las peticiones.

## Decision

Implementaremos o diseñaremos una "función como un servicio" que actúe como coordinadora de servicios con cargas impredecibles y cuyo uso no es muy frecuente.

Llamaremos a una función que determina, basado los metadatos recibidos, la tarea o función que debe usarse para procesar la solicitud. Esta función coordinadora también tiene la capacidad de adaptar o de enriquecer la petición si fuera necesario. Las llamadas entre las funciones se realizan asincrónicamente.

## Consequences

Usaremos una arquitectura asincrónica basada en colas para las invocaciones entre funciones.

Requerimos una plataforma de ejecución de la solución sin servidor.

Implementaremos mecanismos de reintentos y usaremos colas de dead-letter (cola de mensaje fallido) para invocaciones fallidas de funciones. Es importante conocer cual es la estrategia ofrecida por los proveedores de nube para tratar invocaciones de funciones asincrónicas fallidas.

La necesidad de usar comunicaciones asincrónicas entre funciones puede llevar a complejizar el diseño.
