# ADR MSG 0004. Definición de timeouts y de reintentos demorados

Date: 2022-08-23

## Keywords

messaging, message, asincrónica, idempotente, mensaje, cola, reintento, demora, espera, tiempo.

## Status

Accepted

## Context

El tiempo de espera (timeout) es un mecanismo de protección que permite dejar de esperar una respuesta brindando aislamiento de fallas, haciendo que el problema en otro servicio no se convierta en el problema de la aplicación que lo invoca.

Generalmente, los tiempo de esperas se encuentran acompañados de reintentos. Sin embargo, volver a intentar inmediatamente una operación después de una falla tiene pocas consecuencias beneficiosas. Si la operación es parte de un flujo de trabajo crítico donde cancelar o reiniciar el proceso es costoso, es apropiado esperar más tiempo entre intentos, ya que probablemente vuelva a fallar si se vuelve a intentar de inmediato e incluso algunos tipos de fallas pueden potenciarse.


## Decision

Establecemos tiempo de espera (timeouts) y reintentos demorados en el envío de mensajes asincrónicos.

Definir la estrategia de reintentos apropiada en aplicaciones de flujo de trabajo crítico donde cancelar o reiniciar el proceso es costoso es sumamente importante para la estabilidad de la aplicación.

## Consequences

Requerimos aplicar tiempos de espera en envío de mensajes asincrónicos y determinar la estrategia en los reintentos: Incremental, Exponencial o Aleatorización.
