# ADR CLOUD 0006. Escalamiento elástico y automático basado en reglas

Date: 2022-10-28

## Keywords

cloud, escalamiento, horizontal, nodo, elástico, automático, reglas.

## Status

Accepted

Referenced by [ADR CLOUD 0001. Escalamiento horizontal](CLOUD-0001-escalamiento-horizontal.md)

## Context

El escalado horizontal de la aplicación permite aumentar o disminuir los recursos necesarios para hacer frente a los pedidos de los usuarios. Sin la capacidad de escalado, la aplicación no se expande a medida que crece la demanda o no se contrae cuando hay menos demanda.

Escalar horizontalmente en forma manual ayuda a mejorar la gestión de los recursos, pero la automatización puede mejorar la optimización de costos, haciendo que las tareas de escalamiento sean más dinámicas y con un menor esfuerzo.

## Decision

Desarrollaremos reglas de escalamiento automático que posibiliten, basadas en eventos conocidos o en señales de rendimiento, la variación porcentual de los recursos en relación a las necesidades del negocio.

Existen numerosos beneficios del escalado automático con respecto al escalamiento manual:

- Economía de escala: El ajuste automático de los recursos permite que se disponibilicen cuando sean necesarios y se reduzcan cuando el tráfico disminuya.
  
- Rendimientos apropiados: La definición de reglas de escalamiento permite lograr los niveles de rendimiento deseados y asegurarse de que se mantengan.

- Disponibilidad de los servicios: Se garantiza la disponibilidad del servicio durante los picos de tráficos.

## Consequences

Diseñar y desarrollar las aplicaciones aprovechando la administración y el escalado dinámico de recursos.

Definir reglas proactivas de escalamiento teniendo presente las necesidades de recursos habituales como esporádicas durante los días de la semana, fin de semana o eventos especiales. Es decir, calendarizar reglas de escalamiento. Reglas que respondan a las tendencias lo suficientemente temprano para que la capacidad esté disponible a tiempo para la demanda.

Declarar reglas reactivas de escalamiento que permitan responder a rendimiento de los recursos.
