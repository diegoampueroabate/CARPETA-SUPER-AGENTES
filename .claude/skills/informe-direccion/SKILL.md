---
name: informe-direccion
description: Informe de Dirección de AGC Partners. Una página con el estado real de la cartera y las decisiones que esperan a Diego, clasificadas por nivel de autonomía. Actívalo para el brief del lunes, el cierre de mes o cuando haya que ver todo junto.
user-invocable: true
context: fork
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Informe de Dirección

Cierra el ciclo. Las cinco direcciones producen trabajo; este informe lo junta y lo convierte en decisiones. Sin él, el sistema genera material que nadie mira.

**Una página. Que llegue, no que haya que ir a buscarla.**

## De dónde sale cada cosa

| Sección | Fuente |
|---|---|
| Cartera y gasto | `00-Registro-Maestro-Clientes.md` + `ads_get_ad_accounts` |
| Rendimiento por cuenta | conector `mcp__claude_ai_FACEBOOK__*`, con `date_preset` explícito |
| Pipeline | `AGENTE GHL/` y las fichas de prospecto |
| Rentabilidad y cobranza | `finanzacrm/` · conector WASABIL |
| Compromisos abiertos | fichas de cliente y actas de comité |

Nunca uses un `account_id` de memoria. Verifícalo primero.

## Estructura

### 1. Los números, primero

Gasto administrado del período, por cliente, y la concentración. Si algo se movió más de 20% contra el período anterior, dilo en una línea con el número, no con un adjetivo.

**Si no tienes el dato de venta real, declara que falta.** Un informe sin cruce contra venta no emite recomendación de presupuesto — el caso de Óptica Ferreira demostró que el costo por conversación aislado invierte el ranking real.

### 2. Riesgos vivos

Se repiten en cada informe hasta que se cierran, aunque sea aburrido. Hoy abiertos:

- 93% de la inversión administrada es Óptica Ferreira; su cuenta `1946094894848` está en `IN_GRACE_PERIOD`.
- Credenciales de Meta, Google/Gemini y GoHighLevel pendientes de rotación.
- Tratamiento tributario sin confirmar por el contador — bloquea corregir el precio de la propuesta.

Un riesgo que desaparece del informe sin haberse cerrado es peor que no reportarlo.

### 3. Las decisiones — clasificadas por autonomía

El corazón del informe. Cada punto pendiente va en uno de tres niveles:

| Nivel | Qué significa | Ejemplos |
|---|---|---|
| **Dirección decide** | Requiere criterio de Diego. Nada se ejecuta antes | Precio y descuentos · excepción de contrato · aceptar o rechazar un prospecto · cambio de estrategia · escalamiento con un cliente |
| **Dirección aprueba** | Viene resuelto y propuesto; falta el visto bueno | Ajuste de presupuesto en una campaña · propuesta lista para enviar · candidato preseleccionado · documento reemitido |
| **Ya está hecho** | Se ejecutó y solo se informa | Actualización de la bóveda · informes emitidos · seguimiento de leads · documentación de procesos |

Mover una decisión de "decide" a "aprueba" es el trabajo real del sistema: no reemplaza el criterio de Diego, le llega el material listo hasta el punto donde su criterio empieza.

**Nunca subas un nivel por cuenta propia.** Mover presupuesto publicitario, enviar algo a un cliente o firmar sigue exigiendo `ejecuta` / `aplica` / `confirma` / `procede`.

### 4. Qué se hace esta semana

Máximo cinco líneas, cada una con responsable y fecha. Sin responsable no es una decisión, es una intención.

## Cómo se comunica un mal resultado

Del Documento Maestro de Marca §12.1, y aplica también hacia adentro:

1. El dato, directo. "Este mes cerramos 12 de 40. El anterior fueron 18 de 35."
2. Qué pasó, sin excusas ni culpables. Si fue nuestro, se dice.
3. Qué hacemos: decisión concreta, con responsable y fecha.
4. Qué se necesita de Diego.

Nunca se esconde un mal mes ni se maquilla con métricas de vanidad.

## Salida

Se escribe en `00-AGC-Partners/06-Planeacion-y-Finanzas/informes/AAAA-MM-DD-informe-direccion.md` y se resume en pantalla en máximo 8 líneas. El informe completo se lee cuando se quiere el detalle; el resumen es para decidir en un minuto.
