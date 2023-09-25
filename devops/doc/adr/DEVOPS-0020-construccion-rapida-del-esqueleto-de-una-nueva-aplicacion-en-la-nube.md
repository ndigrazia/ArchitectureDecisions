# ADR DEVOPS 0020. Construcción rápida del esqueleto de una nueva aplicación en la nube

Date: 2023-02-15

## Keywords

devops, microservicio, contenedor, código, sin servidor, serverless.

## Status

Accepted

## Context

Cada equipo de desarrollo en una organización es responsable de iniciar la construcción de las nuevas aplicaciones o los nuevos servicios de software sobre los cuales tienen dominio.

Durante el inicio de un nuevo desarrollo, el equipo debe definir el lenguaje de construcción, la estructura del proyecto y como en la mayoría de los lenguajes principales, debe definir cuáles son las bibliotecas más adecuadas para resolver el dominio problema.

Este problema no es exclusivo de las aplicaciones de la nube basada en microservicios. También, puede presentarse en una aplicación monolítica, ya que diferentes programadores pueden usar diferentes componentes o estructuras de proyecto para atacar a un mismo dominio problema.

Son varias las opciones que un equipo puede enfrentar al elegir los componentes a usar en un nuevo proyecto, por lo tanto, el tiempo que toma seleccionar los componentes junto a la estructura que debe tener el proyecto puede ser extenso. Además, del riesgo de elegir un componente que no sea el ideal.

Como resultado, sería sumamente beneficioso poder compartir entre los equipos la experiencia ganada de los mismos en la definición de la estructura del proyecto como en el uso de las librerías que lo forman. 

Vale la pena proveer una estructura básica y un conjunto de librerías o de herramientas, ya que permite potenciar el inicio de los nuevos proyectos, sin tener que lidiar con las complejidades que conlleva la selección de librerías a utilizar junto a la definición del correcto esqueleto del proyecto para atacar el dominio problema.

## Decision

Usaremos platillas (template) de proyecto para crear rápidamente el esqueleto de una aplicación en la nube desde cero.

El uso de plantillas tiene como consecuencia el empleo de herramientas, conocidas como generadores de andamios o scaffolders, cuya responsabilidad es materializar lo definido en la plantilla, tomando el control total sobre la estructura del proyecto.

## Consequences

Hay varias razones por las que debería usar un generador de andamios en el proyecto:

- Velocidad: Se puede generar rápidamente la estructura básica de la aplicación.

- Foco: Permite enfocarse en desarrollar las funcionalidades de la aplicación en lugar de su infraestructura.

- Coherencia: Tener un punto de partida común para todos los proyecto de un dominio problema.

- Reutilizar: Tener una estructura bien definida permite ahorrar tiempo.

Sin embargo, es importante considerar que presenta varios desafíos:

- Empleo y entendimiento (aprendizaje) de la herramienta generadora de andamios.

- Gestión del repositorio donde se almacenarán las plantillas.

- Aprendizaje del lenguaje especifico de dominio para la definición de las plantillas.

- Definición de mecanismos y procedimientos utilizados en la construcción de plantillas.

- Estrategia de gestión de cambios de las plantillas.
