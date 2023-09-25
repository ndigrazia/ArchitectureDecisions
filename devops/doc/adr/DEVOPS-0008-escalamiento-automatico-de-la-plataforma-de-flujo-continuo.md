# ADR DEVOPS 0008. Escalamiento automático de la plataforma de flujo continuo

Date: 2022-12-26

## Keywords

devops, continuo, entrega, despliegue, flujo, proceso, escalamiento, automático.

## Status

Accepted

References [ADR CLOUD 0001. Escalamiento horizontal](../../../cloud/doc/adr/CLOUD-0001-escalamiento-horizontal.md)

References [ADR DEVOPS 0007. Uso de imágenes doradas para el despliegue de las aplicaciones en la nube](DEVOPS-0007-uso-de-imagenes-doradas-para-el-despliegue-de-las-aplicaciones-en-la-nube.md)

## Context

Una arquitectura simple para soportar el flujo de trabajo continuo es implementar un único nodo desde donde se realicen todas las labores. Si bien, es posible escalar el nodo verticalmente para absorber la carga de trabajos, hay un límite hasta donde un nodo puede ser escalado. Por lo tanto, es necesaria una arquitectura diferente que permita poder escalar y soportar proyectos más grandes y complejos.

Distribuir la carga de trabajos entre múltiples nodos de trabajo (workers) es una mejor arquitectura, ya que permite aumentar o disminuir la capacidad de la solución (cantidad de nodos) a medida que las cargas de trabajos disminuyan o aumenten. Es decir, en lugar de desplegar los nodos, que soportan la solución de flujo continuo, en forma independiente, desplegamos los mismos basados en políticas de autoescalamiento que permitan agregar o eliminar nodos en función de variables como: la cantidad de trabajos que esperan en una cola o la utilización del CPU del clúster de trabajo.

## Decision

Implementaremos una plataforma de flujo continuo basada en múltiples nodos de trabajo distribuidos y con políticas de autoescalamiento. 

## Consequences

Para llevar adelante esta definición es necesario contar con imágenes doradas del nodo de trabajo desde donde se pueda aprovisionar la infraestructura, conjuntos de instrucciones (políticas de escalamiento) para ajustar dinámicamente la cantidad de nodos del clúster y dar seguimiento de las variables usada en el escalamiento automático. Esto último puede realizarse con herramientas propias de la plataforma o software de terceros.

Si bien, es necesario tener en cuenta varios puntos a la hora de implementar una plataforma de flujo continuo más escalable, lograrlo, ayudará a hacer a la solución más resiliente a la carga variable de trabajo e independiente de las labores manuales.
