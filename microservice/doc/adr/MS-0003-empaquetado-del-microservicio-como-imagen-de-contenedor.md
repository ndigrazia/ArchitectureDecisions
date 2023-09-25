# ADR MS 0003. Empaquetado del micro servicio como imagen de contenedor

Date: 2022-08-17

## Keywords

microservicio, imagen, despliegue, contenedor.

## Status

Accepted

Referenced by [ADR MS 0001. Reporte de estado de salud en microservicios](MS-0001-reporte-de-estado-de-salud-en-microservicios.md)

Referenced by [ADR MS 0016. Asociar semánticamente cada imagen con una vista en el repositorio de código fuente](MS-0016-asociar-semanticamente-cada-imagen-con-una-vista-en-el-repositorio-de-codigo-fuente.md)

References [ADR MS 0004. Despliegue mediante pipeline](MS-0004-despliegue-mediante-pipeline.md)

References [ADR MS 0005. Único repositorio de fuentes](MS-0005-unico-repositorio-de-fuentes.md)

References [DEVOPS 0007. Uso de imágenes doradas para el despliegue de las aplicaciones en la nube](../../../devops/doc/adr/DEVOPS-0007-uso-de-imagenes-doradas-para-el-despliegue-de-las-aplicaciones-en-la-nube.md)

Referenced by [ADR DEVOPS 0011. Etapas básicas del flujo de trabajo para aplicaciones en la nube basadas en contenedores](../../../devops/doc/adr/DEVOPS-0011-etapas-basicas-del-flujo-de-trabajo-para-aplicaciones-en-la-nube-basadas-en-contenedores.md)

## Context

Existen cuatro opciones para la implementación de servicios:

- Paquetes específicos, como por ejemplo, Java JAR o WAR.
- Máquinas virtuales.
- Contenedores.
- Serverless.

La implementación como paquetes presenta varios inconvenientes como: falta de encapsulación del stack tecnológico, no restringe los recursos consumidos por la instancia del servicio, falta de aislamiento de ejecución entre múltiples instancias del servicio y además, carece de mecanismos para determinar automáticamente dónde alocar las instancias del servicio.

Por otro lado, la implementación en máquina virtual genera despliegues relativamente lentos, mayores gastos en administración de las máquinas virtuales y carece de eficiencia en la utilización de los recursos.

Con respecto a la implementación con funciones Serverless, es una forma extremadamente conveniente de implementar servicios pero presenta problemas de latencia, debido a que se ejecuta dinámicamente su código, haciendo que algunas solicitudes tarden demasiado en responderse esperando el inicio de la aplicación. Asimismo, dado que se soporta sobre un modelo de programación basado en eventos, no es adecuada a todos los servicios o a servicios de tiempos de ejecución larga (long-running services).

Finalmente, si bien los contenedores requieren tareas administrativas sobre las imágenes del contenedor como parchear el sistema operativo o actualizar el runtime, cuentan con numerosos beneficios como: encapsulación del stack tecnológico, las instancias del servicio están aisladas, permiten despliegues rápidos y los recursos de las instancias del servicio están limitados.

## Decision

Empaquetamos el microservicio como una imagen de contenedor.

Para que las aplicaciones puedan ser ejecutadas en un contenedor se requiere que la misma puede ser empaquetada en una imagen de contenedor.

Los contenedores son un mecanismo de implementación moderno y liviano que simplifica el desarrollo, la prueba y el despliegue de aplicaciones en múltiples entornos, requiriendo menos recursos del sistema que los entornos de máquinas virtuales tradicionales y, permitiendo que las aplicaciones se implementen, reparen o escalen más rápidamente.

Generar una imagen de contenedor al momento de la compilación permite disponer de componentes inmutables que garantizan un entorno consistente que va desde desarrollo hasta producción. 

Mayor facilidad y eficiencia al crear imágenes de contenedor en vez de máquinas virtuales.

## Consequences

Requerimos el uso de una imagen base de construcción del contenedor que describe el entorno de ejecución, empleo del fuente de la aplicación a ser inyectada, uso de un proceso de construcción que transforma el código fuente en una imagen de contenedor ejecutable y versionada basada en la imagen base de construcción del contenedor.
