# ADR FAAS 0008. Patrones de carga predecibles

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, carga, predecible, patron.

## Status

Accepted

Referenced by [ADR FAAS 0010. Webhook entrantes](FAAS-0010-webhook-entrantes.md)

Referenced by [ADR FAAS 0011. Autenticación de usuarios](FAAS-0011-autenticacion-de-usuarios.md)

Referenced by [ADR FAAS 0012. Tareas en segundo plano](FAAS-0012-tareas-en-segundo-plano.md)

Referenced by [ADR FAAS 0013. Recopilar datos de transmisión continua](FAAS-0013-recopilar-datos-de-transmision-continua.md)

## Context

Las aplicaciones de software pueden tener patrones de uso predecibles y/o impredecible. Es decir, que hacen uso intensivo o no de cómputo. 

Los proveedores en la nube ofrecen diversas modalidades de pagos para los servicios que los mismos ofrecen.

Una de las características más atractivas de la solución sin servidor es que no se paga por el tiempo de inactividad. Es decir, si el servicio no se usa durante un período no se facturará por el mismo. Como contrapartida, los servicios soportados por soluciones basadas en servidores pagarán aun cuando los mismos no estén recibiendo peticiones. Podemos, como solución más extrema, apagarlos en los periodos de inactividad para ahorrar dinero pero el servicio no tendrá disponibilidad ante peticiones poco frecuentes, llevando a la necesidad de disponer un estado mínimo de funcionamiento y como consecuencia, el pago del mismo.

La solución de pago por uso ofrecida por las soluciones sin servidor parece sumamente atractiva, ya que se paga por el tiempo de uso. Sin embargo, este modelo puede ser potencialmente más caro ante carga de trabajos que hacen uso de una cantidad predecible y estable de cómputo, haciendo que las soluciones que emplean servidores sean más seductoras.

## Decision

No usaremos una "función como un servicio" para procesar cargas predecibles de trabajo.

El uso de funciones para el procesamiento de cargas predecibles o de uso frecuente no es el más adecuado, ya que costará más que otras soluciones basadas en servidores. Como por ejemplo, la tecnología de contenedores.

Resulta más costoso, en la mayoría de los casos, el uso de una solución sin servidor cuando existe un procesamiento predecible y continuo. Sin embargo, es importante analizar los gastos de mantenimiento y de gestión de la solución basada en servidor a fin de determinar si el camino hacia una solución sin servicio es el más adecuado.

## Consequences

Requerimos el uso de soluciones basadas en servidores para el procesamiento de cargas predecibles o de peticiones de uso frecuentes.

Requerimos una plataforma de ejecución y de distribución de la solución de basada en servidor.

Las soluciones basadas en servidores requieren actividades de mantenimiento y de soporte.  
