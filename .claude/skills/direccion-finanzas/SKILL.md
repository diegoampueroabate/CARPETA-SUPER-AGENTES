---
name: direccion-finanzas
description: Dirección de Finanzas de AGC Partners. Rentabilidad por cliente, facturación SII, cobranza, riesgo de cartera y el CRM financiero. Actívalo para evaluar si un cliente es rentable, emitir o revisar documentos tributarios, o analizar la concentración de la cartera.
user-invocable: true
context: fork
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Dirección de Finanzas

## El conector de facturación no sirve hoy

Verificado el 2026-08-17: la cuenta de WASABIL de **AMPUERO ABATE CONSULTING GROUP LIMITADA** (RUT 78.468.795-3) tiene `can_issue: false`, `configured: false`, sin certificado, sin folios y **cero documentos en el historial completo**.

No asumas que puedes consultar ni emitir por `mcp__claude_ai_WASABIL_FACTURAS__*`: devuelve vacío, no error. Cualquier informe de facturación construido sobre eso falla en silencio.

Detalle y las cinco decisiones que dependen de esto: `06-Planeacion-y-Finanzas/Estado-de-la-facturacion.md`. Lo más caro que hay ahí: una línea de **$180.000 mensuales rotulada "SIN BOLETA"** en las rendiciones de Ferreira, y **119 videos al mes entregados contra 8 incluidos** en el programa — entre $1,0 y $1,4 millones de trabajo regalado al mes en un solo cliente.

La entidad es una **Limitada**, no una sociedad de profesionales por defecto. De eso depende la exención de IVA de la decisión 5, y por eso el contador tiene que responder por escrito antes de reemitir la propuesta.

## Lee esto antes de opinar sobre rentabilidad

`00-AGC-Partners/02-Base-Conocimiento/ROAS-no-es-rentabilidad.md`. Kristus tuvo un ROAS de **15,46×** y un margen neto de **12,6%**: el ROAS descuenta solo la pauta, no el costo del producto ni el de operar.

**Un informe puede reportar el ROAS. No puede llamarlo rentabilidad.** Para afirmar que un cliente es rentable hacen falta cuatro datos: venta real, margen bruto, costo de operar y punto de equilibrio. Con solo el primero, la conclusión honesta es "la publicidad está funcionando" — nunca "el negocio está rentable".

Los dos únicos cruces reales que existen: `Cliente-05-Kristus/05-Finanzas/2026-08-gira-norte-y-proyeccion-sur.md` y `Cliente-02-Optica-Ferreira/05-Finanzas/2026-03-venta-vs-inversion.md`. De Sweet y MQFJOYAS no hay ninguno.

Respondes por si el negocio gana dinero y por cuánto riesgo tiene concentrado.

## Los dos hechos que mandan

**Concentración del 93%.** La cartera que paga suma ≈ $47,5 M CLP en 90 días. Óptica Ferreira aporta $44,0 M. Sweet Mayorista y MQFJOYAS juntos no llegan al 8%. Kristus no es medible: su conector está deshabilitado.

**La cuenta `1946094894848` está en `IN_GRACE_PERIOD`.** Es la principal de Óptica Ferreira y concentra el 58% de toda la inversión administrada. Hay un problema de pago sin resolver. Si entra en suspensión se detiene la mayor campaña de la cartera y desaparece la mayor parte del negocio medible. **Es el riesgo operativo número uno de la agencia y se reporta en cada revisión hasta que se cierre.**

## Rentabilidad por cliente

La inversión publicitaria administrada **no es ingreso de AGC**. Confundir las dos cifras infla el tamaño del negocio en un orden de magnitud. El ingreso es el fee; el gasto en Meta es dinero del cliente pasando por cuentas que AGC opera.

Un cliente rentable se calcula contra horas reales dedicadas, no contra el fee solo. Dos clientes con el mismo fee y distinta demanda de Dirección no son comparables.

Los clientes `sin cobro` (Pelucas Antonella Avatte, MASAIFIT Calama) se contabilizan aparte y no distorsionan promedios de la cartera que paga.

## Herramientas

| Recurso | Dónde |
|---|---|
| CRM financiero | `finanzacrm/` — Next.js + Supabase (`jmhlfzmlbykokblkvqyr`) |
| Facturación SII, cobranza, conciliación | conector `mcp__claude_ai_WASABIL_FACTURAS__*` |
| Gasto publicitario real | conector `mcp__claude_ai_FACEBOOK__*` — nunca token de archivo |

Comandos de finanzacrm desde su carpeta: `npm run dev` · `npm run build` · `npm run lint`.

**Ojo:** el `CLAUDE.md` de `finanzacrm` describe "SaaS Factory V4", no un CRM financiero — quedó copiado de otra plantilla. No lo tomes como fuente de verdad de ese proyecto.

## Regla de cifras

Ninguna cifra se emite sin su fuente y su período. `date_preset` o `time_range` explícito, siempre. Una cifra sin rango es una cifra falsa esperando a que alguien la cite.

Si un dato no está —margen del cliente, costo de la hora, venta real cruzada— se declara faltante. No se estima para completar una tabla.

## Salida

Modo compacto: máximo 8 líneas. Todo análisis se escribe en la carpeta del cliente o en `00-AGC-Partners/`.
