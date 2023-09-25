# ADR CTR 0011. Prevención de fuga de información confidencial durante la descarga de librerías de terceros

## Keywords

containerizing, container, imagen, uso, contenedor, producción, perdida, confidencial,  vulnerabilidad, confiable.

## Status

Accepted

## Context

Durante el proceso de construcción de la imagen nuestros contenedores pueden requerir de funcionalidades exteriorizadas en librerías o en paquetes de terceros. Existe la posibilidad que estas dependencias, que constituirán nuestra imagen, se encuentren alocadas en repositorios (maven, npm, etc.) protegidos mediante clave. En estos casos, necesitamos emplear un mecanismo para disponibilizar dichas claves durante el proceso de construcción y así, permitir las descargas de sus dependencias.

Dependiendo del mecanismo usado para disponibilizar las claves requeridas por los repositorios privados, podemos provocar la perdida información confidencial.

## Decision

Evitamos emplear cualquier mecanismo o práctica que permita recuperar, luego del proceso de construcción de las imágenes, las claves disponibilizadas para el acceso a los repositorios de dependencias privados.

## Consequences

Requerimos evitar el uso de variables de ambientes como medio de disponibilizar las claves.

Requerimos evitar el uso de argumentos como práctica de abastecimiento las claves.

Requerimos la estrategia de construcciones de múltiples etapas (Multi-stage) como mecanismo de mitigación de este problema. Para ello, en la primera etapa de construcción de la imagen productiva, usaremos una imagen temporal de construcción (o build image). En ella, disponibilizaremos todo lo que necesitamos. Esto es, la instalación de paquetes o herramientas de terceros necesarias para la ejecución de la aplicación. Sobre la misma, continuaremos con el proceso de construcción (compilación, empaquetado, etc.). Luego, cuando el proceso de la primera fase este finalizado, haremos uso de una segunda imagen, la cual dará inicio a la segunda fase de construcción. En esta segunda imagen, copiaremos todo lo construido en la fase previa, optimizamos y publicamos la imagen resultante (imagen productiva) en un registro de imágenes, si existiera uno.

Finalmente, la primera imagen, empleada como parte del proceso de construcción de la aplicación, se descarta y se limpia, evitando el recupero de cualquier información confidencia

