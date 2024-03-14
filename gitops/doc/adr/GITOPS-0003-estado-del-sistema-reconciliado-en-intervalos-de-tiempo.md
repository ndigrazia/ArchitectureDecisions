# ADR GITOPS 0003. Estado del sistema reconciliado en intervalos de tiempo

Date: 2024-03-06

## Keywords

gitops, devops, estado, deseado, declarativo, declarativa, reconciliado, tiempo.

## Status

Accepted

References [ADR GITOPS 0001. Estado deseado del sistema expresado de forma declarativa](GITOPS-0001-estado-deseado-del-sistema-expresado-de-forma-declarativa.md)

References [ADR GITOPS 0002. Estado deseado inmutable y versionado](GITOPS-0002-estado-deseado-inmutable-y-versionado.md)

Referenced by [ADR GITOPS 0008. Método de despliegue activado por CI y adueñado por GitOps](GITOPS-0008-metodo-de-despliegue-activado-por-ci-y-adueñado-por-gitops.md)

## Context

El "estado deseado" de un sistema representa la meta o el resultado que se busca alcanzar para que el sistema funcione de manera eficiente y cumpla con nuestros objetivos. La sincronización del estado deseado es fundamental para garantizar que la realidad del sistema refleje de manera precisa y coherente los objetivos y necesidades establecidas.

## Decision

Reconciliaremos el "estado real" del sistema con su "estado deseado" a intervalos de tiempo regulares.

Si se identifica una discrepancia entre el "estado deseado" y el "estado real" en ejecución, se toman medidas para corregir y ajustar automáticamente el sistema.

Extraeremos las declaraciones del "estado deseado" desde un repositorio o fuente de verdad.

A diferencia de un flujo de CI-CD, no hay un webhook que debe ser invocado. En cambio, hay un ciclo regular de reconciliación.

## Consequences

Emplearemos una herramienta GitOps para realizar la sincronización del "estado real" y el "estado deseado" del sistema. 

La conciliación entre los "estados deseados" y los "estados en ejecución" en un sistema ofrece una variedad de beneficios clave para asegurar que el sistema funcione de manera efectiva y alineada con los objetivos establecidos. Algunas consideraciones importantes:

- Garantiza que el sistema esté siempre alineado con los objetivos y requisitos establecidos, lo que contribuye al éxito general del proyecto o del negocio.

- Asegura que el sistema sea consistente y confiable, proporcionando una experiencia más predecible y satisfactoria para los usuarios.

- Contribuye a la eficiencia operativa al minimizar desviaciones no planificadas y optimizar el rendimiento del sistema.

Por otro lado, puede presentar algunas desventajas como la necesidad de herramientas especializadas y tiempo dedicado a las mismas. Sin embargo, consideramos que los beneficios de la conciliación superan sus desafíos. 

