# ADR GITOPS 0009. Entornos de configuración separados en directorios no en ramas

Date: 2024-03-14

## Keywords

gitops, devops, configuración, entorno, directorio, rama.

## Status

Accepted

References [ADR GITOPS 0007. Organización en múltiples repositorios para diferentes ambientes o clústeres](GITOPS-0007-organizacion-en-multiples-repositorios-para-diferentes-ambientes-o-clusteres.md)

## Context

La organización de entornos de configuración puede seguir diferentes técnicas, como el uso de ramas (branches) o la separación en directorios dentro de una misma rama. Ambas aproximaciones tienen sus ventajas y desventajas, y la elección entre una u otra depende de varios factores, incluyendo las preferencias del equipo de desarrollo, la complejidad del proyecto y las herramientas utilizadas.

En el uso de ramas se utilizan ramas separadas en el repositorio de código para mantener las configuraciones específicas de cada entorno (por ejemplo, desarrollo, pruebas, producción).

La separación en directorios en una misma rama es un enfoque donde las configuraciones se mantienen en una sola rama, pero se organizan en directorios separados para cada entorno.

## Decision

Separamos la configuración de los entornos en directorios diferentes en una misma rama.

En lugar de mantener todas las configuraciones en ramas separadas, se separan en directorios para una mejor organización y gestión.

## Consequences

Creamos directorios separados para cada entorno dentro de una sola rama del repositorio de código. 

Gracias a la separación en directorios en una misma rama podemos lograr una estructura más clara y organizada en el repositorio de código. Cada directorio puede contener los archivos de configuración relevantes para un entorno específico. Cada directorio de configuración puede adaptarse específicamente a las necesidades del entorno al que pertenece. Por ejemplo, las configuraciones de desarrollo pueden incluir herramientas de depuración adicionales o configuraciones de registro detalladas que no serían necesarias en producción.

El uso de ramas para mantener configuraciones específicas de cada entorno puede complicar el proceso de promoción de un entorno a otro. Cuando se utilizan ramas separadas para cada entorno, promover cambios de un entorno a otro puede requerir un proceso más elaborado y propenso a errores.

En resumen, la organización de entornos de configuración separados en directorios ofrece una forma eficaz de gestionar configuraciones específicas para diferentes entornos de desarrollo de software, lo que proporciona claridad, independencia, facilidad de mantenimiento y personalización.

