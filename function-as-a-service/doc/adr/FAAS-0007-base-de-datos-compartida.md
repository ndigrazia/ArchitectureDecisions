# ADR FAAS 0007. Base de datos compartida

Date: 2023-03-06

## Keywords

faas, serverless, función, sin servidor, servicio, invocación, dato, compartida.

## Status

Accepted

## Context

La "función como un servicio" es sin estado (stateless) por naturaleza sin embargo, muchas funciones podrían necesitar alguna base de datos para almacenar su estado. Se puede agilizar el desarrollo de una función empleando una base datos compartida pero como consecuencia, se vuelve mas arduo el trabajo de definir claramente los limites entre las aplicaciones que la utilicen.

Al mismo tiempo que una base de datos compartida comienza a entrelazar las aplicaciones se vuelve más difícil realizar cambios sin provocar mayores impactos y, posiblemente aumentarán los bloqueos a medida que la base de datos se convierta en un cuello de botella del sistema, ya que no puede escalar al ritmo de las necesidades de los servicios que esta soporta.

## Decision

No implementaremos una "función como un servicio" que haga uso de una base de datos compartida.

Una base de datos compartida no promueve la resiliencia y la escalabilidad. A su vez, fomenta el acoplamiento entre los servicios o las aplicaciones que la utilizan, haciendo que toda su plataforma de negocio este prácticamente fuera de línea ante cualquier caída o perdida del servicio de datos.

## Consequences

Diseñaremos e implementaremos funciones sobre contextos de negocio bien delimitados es decir, que cada función posea sus propios datos, aquellos necesarios para resolver el problema para la cual fue creada.

Usaremos mecanismos de comunicación asincrónicos (eventos o mensajes) para comunicar cambios en el estado de la función que requieran ser conocido por otros componentes del sistema.

Usaremos dos tipos de impulsores o drivers para llevar adelante el desacoplamiento de la base de datos compartida.

Los Impulsores de Separación justifican la separación de datos y los Impulsores de Agregación justifican mantener los datos juntos. Mediante el análisis de ventajas y desventajas entre estas dos fuerzas podremos obtener la granularidad correcta de los datos que estarán asociados a la función.

Impulsores de Separación:

- Negocio: Desacoplamos la base de datos de acuerdo al contexto especifico del negocio.
  
- Control de Cambio: Desacoplamos la base de datos de acuerdo al impacto de sus cambios.
  
- Escalabilidad: Desacoplamos la base de datos de acuerdo a las distintas necesidades de escalabilidad.
  
- Tolerancia a fallos: Desacoplamos la base de datos de acuerdo a las necesidades de tolerancia a fallos.
  
- Tipo de datos: Desacoplamos la base de datos de acuerdo al tipo de base de datos (clave-valor, documental, familia columnar, etc.) mas adecuado para resolver el problema.
  
Impulsores de Agregación:

- Consistencia e integridad: Acoplamos datos en un base de datos si es requerido garantizar la consistencia e integridad de los mismos en una unidad atómica de trabajo transaccional. 

- Relación: Acoplamos datos en un base de datos si las relaciones entre ellos son necesarias para preservar el funcionamiento requerido de los componentes de software que lo usen.

Desacoplar una base de datos es difícil debido a que los datos son generalmente el activo más importante de la empresa, haciendo que el riesgo de interrupción del negocio aumente a medida que se desestructuran los datos.
