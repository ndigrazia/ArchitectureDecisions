# ADR DEVOPS 0017. Almacenamiento centralizado de los registros de la plataforma de flujo continuo

## Keywords

devops, registro, log, infraestructura, continuo, entrega, despliegue, flujo, proceso, almacenamiento, centralizado, central.

## Status

Accepted

## Context

Los registros (logs) generados en la plataforma de flujo continuo brindan mucha información a la hora de analizar e identificar las causas raíces de la falla del flujo de trabajo. Los registros contienen datos como el nombre del flujo de trabajo, el tiempo de ejecución, el resultado de la ejecución, motivos de falla de la ejecución, entre otras cosas.

La plataforma de flujo continuo puede almacenar sus registros sobre archivos guardados dentro de la propia plataforma. Sin embargo, dependiendo de la configuración realizada o los recursos disponibles, los registros más antiguos podrían perderse. Es por este motivo, que se debe conservar los registros en una plataforma de registro centralizada y así, disponer del total de registros en futuras auditorías y diagnósticos de problemas.

## Decision

Conservaremos los registros generados en la plataforma de flujo continuo en una plataforma de registro centralizada.

Esta decisión facilitará futuras auditorías y diagnósticos de problemas.

La solución de registro centralizada se puede dividir en las siguientes partes:

- Lightweight shipper: Supervisa los archivos de registro o las ubicaciones que se especifiquen, recopilando eventos de registros y enviándolos al procesador de registros.

- Log processor: Filtra y procesa los registros provenientes de fuentes generadoras de eventos, enviando los resultados a un almacenamiento de datos.

- Data store: Guarda los datos de los registros para su posterior búsqueda.

- Log frontend: Interfaz visual por la cual el usuario realiza consulta o construye dashboard para el análisis de los registros. Este componente se conecta con el almacenamiento de datos para realizar su función.

## Consequences

El uso una solución de registro centralizada ahorra muchas horas valiosas tanto para el equipo de soporte como para los desarrolladores en el diagnostico como en la resolución de problemas. Sin embargo, para alcanzar este beneficio, se debe considerar los siguientes desafíos:

- La elección del software usado como plataforma de registro centralizada.
  
- Habilidades requeridas en los administradores para configurar y aprovisionar la infraestructura de la solución.
  
- Definición y configuración de los procesos de filtrado y de procesamiento de los registros.

- Creación de pizarras (dashboard) basadas en la información almacenada de los registros.
