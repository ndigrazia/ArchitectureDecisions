# ADR CLOUD 0009. Detección de respuestas de "servicio ocupado"

Date: 2022-11-01

## Keywords

cloud, integración, respuesta, recursos, servicios, ocupado.  

## Status

Accepted

Referenced by [ADR CLOUD 0010. Tratamiento de respuestas "servicio ocupado"](CLOUD-0010-tratamiento-de-respuestas-servicio-ocupado.md)

## Context

La plataforma en la nube sobre la que se despliegan las aplicaciones modernas es la responsable de administrar de manera transparente la competencia de los servicios y/o recursos para satisfacer las necesidades de los grupos de usuarios. Las demandas realizadas son variables y dinámicas a través del tiempo por lo tanto, la plataforma proactivamente decidirá distribuir los recursos y/o servicios de acuerdo a los requerimientos realizados.

Puede ocurrir, durante el proceso de reasignación de capacidades, que el acceso a los recursos y/o servicios compartidos experimenten fallas transitorias o retornen señales de ocupado. Generalmente, muchas de las fallas transitorias o respuestas con señales de ocupado son producidas por problemas en el hardware o por la ausencia momentánea de los servicios, haciendo sumamente importante poder detectar estos escenarios para luego responder adecuadamente, ya que en caso contrario, se estaría afectando la estabilidad del sistema, la cual no se garantiza solamente con los servidores o las aplicaciones funcionando, sino que también, permitiendo al usuario hacer su trabajo.

## Decision

Identificamos los escenarios dentro de la aplicación donde pueden ocurrir fallas transitorias o señales de ocupado, debido a problemas en el hardware o a la ausencia momentánea de los servicios.

Las aplicaciones contienen conexiones que la vinculan con servicios de la plataforma (base de datos, gateways, brokers, etc.). Todas estas conexiones son puntos de integración, y cada uno de ellos es una posible zona de dolor para la aplicación. De hecho, cuanto más servicios pequeños tengamos o más APIs usemos para integrarnos, mas posibles problemas tengamos que enfrentar. Los puntos de integración son el asesino número uno de las aplicaciones. Cada socket o llamada remota que realicemos puede colgar o colapsar el sistema.

Cada punto de integración eventualmente fallará de alguna manera y se necesita estar preparado para ese fracaso.

## Consequences

Complejidad en el desarrollo y en el diseño de la aplicación, ya que se debe considerar:

    - Detectar los puntos en la aplicación donde pueden suceder fallas transitorias por acceso a servicios y/o recursos de la nube.

    - Analizar e identificar como son informadas las fallas transitorias o señales de ocupado por la plataforma en la nube.

    - Discriminar las fallas transitorias o señales de ocupado del resto de las fallas.

    - Aplicar patrones para evitar problemas de puntos de integración.

