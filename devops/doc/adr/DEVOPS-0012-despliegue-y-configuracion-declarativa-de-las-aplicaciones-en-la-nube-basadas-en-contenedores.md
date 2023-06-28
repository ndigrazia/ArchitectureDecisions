# ADR DEVOPS 0012. Despliegue y configuración declarativa de las aplicaciones en la nube basadas en contenedores

## Keywords

devops, aprovisionamiento, entrega, despliegue, recurso, código, declarativo, contenedor, microservicio.

## Status

Accepted

## Context

Tradicionalmente el despliegue y la configuración de las aplicaciones era realizada por procesos manuales que requerían de mano de obra para completarse. Estas prácticas estaban acompañadas de pasos establecidos en documentos que deben seguirse para concluir el despliegue y la configuración de las aplicaciones.

Usar las prácticas de las aplicaciones tradicionales en aplicaciones en la nube y en particular, en soluciones basadas en contenedores que requieren cambios más frecuentes, implican mayor cantidad de tiempo en el aprovisionamiento de la aplicación y como consecuencia, demora en el tiempo del lanzamiento de la solución al mercado. Asimismo, los procesos manuales tienen como resultado mayores posibilidades de cometer errores por la implicancia del propio procedimiento.

En las aplicaciones más modernas en la nube todo el conocimiento de su despliegue y de su configuración (estado del sistema) queda definido como código en un repositorio de fuentes que actúa como la fuente de la verdad. En este escenario el objetivo del equipo de operaciones es definir el estado deseado como código y almacenarlo en el repositorio de fuentes, evitando ejecutar manualmente cualquier tipo de comandos.

## Decision

Implementaremos el despliegue y la configuración de aplicaciones basadas en contenedores mediante un enfoque declarativo en archivos de código.

Se usa un repositorio de fuentes como la fuente confiable de la información. Cualquier modificación en dicha información resultará en cambios automáticos en su infraestructura asociada.

Esta práctica constituye la base del patrón de Infraestructura como Código.

La información despliegue y la configuración es declarada en un archivo versionado.

## Consequences

El empleo de esta práctica requiere considerar ciertos aspectos:

- Empleo de una herramienta de versionado de código.

- Definición de la estrategia usada en el control de cambios en las fuentes.

- Entendimiento del lenguaje de declaración usado.

- Entendimiento de la herramienta usada para el despliegue y la configuración desde el código.
