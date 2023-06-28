# ADR FAAS 0019. Cortacircuitos

## Keywords

faas, serverless, función, sin servidor, servicio, cortacircuitos, circuit breaker, patrón.

## Status

Accepted

## Context

Tarde o temprano, durante la ejecución del sistema, se producirá algún fallo que ocasione la interrupción de su flujo normal. Se dice que un sistema tiene resiliencia cuando cuenta con la capacidad de recuperarse de las fallas y continua funcionando a pesar de las mismas.

Los patrones de resiliencia ofrecen mecanismos que ayudan a nuestros sistemas a estar preparados ante situaciones de fallas.

El patrón Cortacircuitos (Circuit Breaker) es uno de los mecanismos que evita intentar ejecutar repetidamente una operación que posiblemente no funcione.

Existen diferentes formar de implementar este patrón.

## Decision

Implementaremos o diseñaremos una "función como un servicio" como cortacircuitos para proteger servicios sincrónicos con cargas impredecibles y cuyo uso no es muy frecuente.

Cuando la cantidad de fallas alcanza un determinado limite, abrimos el circuito y retornamos errores al cliente sin llamar al servicio original. Luego de un tiempo de espera, enviamos algunas solicitudes para ver si el servicio responde correctamente. El resto de las peticiones reciben un error. Si el servicio opera exitosamente, comenzamos a pasar todo el tráfico. En caso contrario, volvemos a repetir el proceso. 

Considerar aumentar el tiempo de espera entre intentos de reintento.

La "función como un servicio" actúa como cortacircuito, protegiendo al servicio interno o externo. 

## Consequences

Requerimos una plataforma de ejecución de la solución sin servidor.

Requerimos una solución de API Gateway que dirija el trafico al cortacircuito.

Requerimos lógica de cortacircuito con alta performance y alta disponibilidad.

Requerimos una solución tecnológica para persistir el estado del cortacircuito.
