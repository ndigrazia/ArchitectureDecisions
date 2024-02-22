# ADR GEN 0001. Uso de ADR para registro de decisiones de arquitectura

Date: 2023-05-10

## Keywords

adr, log, decisión, registro, documento.

## Status

Accepted

References [ADR GEN 0002. Formato usado en el documento ADR](GEN-0002-formato-usado-en-el-documento-adr.md)

## Context

La captura de las decisiones de arquitectura, junto con su contexto y sus consecuencias, es un aspecto crucial para el éxito de un proyecto o producto de software. Es por ello, un requisito fundamental contar con un documento estructurado que sirva como registro central de estas decisiones, proporcionando una referencia clara y documentada para todos los miembros del equipo. 

## Decision

Utilizaremos ADR (Registro de Decisiones de Arquitectura) como mecanismo de registro de las decisiones de arquitectura.

Crearemos un ADR por cada decisión significativa de arquitectura que tenga impacto en un proyecto o en un producto de software. Los ADRs deben registrar las decisiones de Arquitectura en los siguientes aspectos:

*Estructurales*: Definir la estructura arquitectónica adoptada, incluyendo patrones como microservicios u otras decisiones de diseño que afecten la arquitectura u organización del sistema.

*Requisitos no funcionales*: Especificar los requisitos no funcionales relevantes, como medidas de seguridad, alta disponibilidad y tolerancia a fallos, que influyan en la arquitectura del sistema.

*Dependencias*: Describir las dependencias entre componentes del sistema, abordando el nivel de acoplamiento y cómo afectan la interacción entre módulos o servicios.

*Interfaces*: Detallar las interfaces del sistema, tanto las API como los contratos publicados, para garantizar la coherencia y la comprensión clara de cómo se comunican los diferentes componentes.

*Técnicos*: Especificar las técnicas de construcción adoptadas, incluyendo bibliotecas, frameworks, herramientas y procesos seleccionados para el desarrollo del software, con el fin de proporcionar una guía coherente en el enfoque de construcción del sistema.

## Consequences

Si el equipo de arquitectura decide abandonar el uso del Registro de Decisiones de Arquitectura (ADR), se corre el riesgo de perder el valioso contexto asociado con las decisiones de Arquitectura tomadas a lo largo del tiempo. El ADR no solo actúa como un repositorio de decisiones pasadas, sino que también documenta el razonamiento y el entorno que influyeron en esas decisiones. 

A continuación, se destacan algunas de las consecuencias negativas de prescindir de los ADRs:

*Pérdida de contexto*: La información contextual clave que rodea a las decisiones de Arquitectura se perdería, lo que dificultaría la comprensión completa de las razones detrás de las decisiones tomadas.

*Dificultad en la toma de decisiones futuras*: Sin un historial documentado, el equipo podría enfrentar dificultades al intentar tomar decisiones coherentes y consistentes en el futuro, ya que carecerían del contexto necesario.

*Desafíos en la comunicación*: La falta de un registro estructurado podría resultar en problemas de comunicación dentro del equipo. Los nuevos miembros o aquellos que no estuvieron presentes en el momento de la toma de decisiones podrían tener dificultades para comprender las decisiones tomadas.

*Riesgo de repetir errores*: Sin un historial claro de decisiones y sus consecuencias, existe el riesgo de repetir errores anteriores o de tomar decisiones subóptimas.

*Impacto en la mantenibilidad*: La capacidad de mantener y evolucionar la arquitectura del sistema puede verse comprometida, ya que las decisiones antiguas podrían no ser comprensibles o estar mal interpretadas.

En resumen, la decisión de abandonar el uso del ADR podría tener implicaciones significativas en la coherencia, la comprensión y la eficacia del proceso de toma de decisiones de Arquitectura. Mantener un registro de las decisiones es una práctica valiosa para preservar el conocimiento acumulado y mejorar la gestión de la arquitectura a lo largo del tiempo.

