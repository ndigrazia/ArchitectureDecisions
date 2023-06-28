# ADR MESH 0001. Uso de sidecar para acoplamiento operativo

## Keywords

mesh, sidecar, malla de servicios.

## Status

Accepted

## Context

Cada servicio en la arquitectura de microservicios requiere operaciones de infraestructura comunes, transversales y consistentes. Dejar la responsabilidad de su definición y su actualización en los equipos de desarrollo generará inconsistencias y problemas de coordinación.

## Decision

Usaremos un componente sidecar junto con una malla de servicios para consolidar el acoplamiento de las funciones transversales de infraestructura.

El componente sidecar realiza funciones transversales que dan soporte a la función core implementada en el servicio principal.

El equipo que tendrá el rol de infraestructura será el propietario y mantendrá el sidecar para que los restantes equipos de desarrollo de servicios puedan utilizarlo. El sidecar ofrecerá los siguientes servicios:

- Recopilación de métricas.
- Trazabilidad distribuida.
- Monitoreo.
- Autenticación (TLS y autenticación en la malla).
- Autorización (control de acceso a los servicios en la malla).
- Circuit Breaker.
- Requests Timeout.
- Requests Retry.
- Duplicación (Mirroring).
- Estrategia de despliegue (Canary, A/B, Blue Green).

## Consequences

No se agregará lógica de dominio en el sidecar, ya que fomenta el acoplamiento.
