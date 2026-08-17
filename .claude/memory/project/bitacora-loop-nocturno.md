---
name: bitacora-loop-nocturno
description: Qué se construyó en el loop de la noche del 16 al 17 de agosto de 2026
metadata:
  type: project
---

# Bitácora — noche del 16-ago-2026

## Construido

**Fase 1 — fuente de verdad: cerrada.** Registro Maestro reescrito contra la API de Meta: 20 cuentas cruzadas, cartera definida en 4 clientes que pagan + 2 sin cobro. Las 9 fichas de cliente tienen frontmatter YAML con `nombre_canonico`, `modalidad`, `meta_account_ids` y `gasto_90d_clp`. `AGENTE ADS MANAGER/CLAUDE.md` corregido: se eliminaron los dos `account_id` inexistentes que hacían fallar consultas en silencio.

**Fase 2 — las cinco direcciones: escritas.** En `CARPETA SUPER AGENTES/.claude/skills/`:

| Dirección | Cubre |
|---|---|
| `direccion-marketing` | Meta Ads, copy, creativos, contenido |
| `direccion-ventas` | pipeline GHL, propuestas, cierre |
| `direccion-operaciones` | SOPs, incorporación, reportería, integridad de la bóveda |
| `direccion-rrhh` | reclutamiento, delegación, frontera de criterio |
| `direccion-finanzas` | rentabilidad, SII, riesgo de cartera |

Cada una arranca leyendo el Registro Maestro, respeta "por defecto solo recomendar" y escribe su resultado en la bóveda en vez de devolverlo solo en pantalla. Los 240+ skills existentes se referencian desde su repo de origen — no se copian, porque duplicados divergen en un mes.

**Fase 3 — memoria persistente: sembrada.** `.claude/memory/` con índice y las categorías `user/`, `feedback/`, `project/`, `reference/`.

**Fase 4 — `/onboarding-cliente`: escrito.** `.claude/skills/onboarding-cliente/SKILL.md`. Exige el nombre canónico confirmado antes de crear nada, escribe el Registro Maestro antes que la carpeta, deja `meta_account_ids: []` vacío en vez de inventar un ID, y trae la secuencia para el prospecto que **no** tiene cuenta publicitaria (BM a nombre del cliente, no de AGC — si la relación termina, el histórico y el pixel se quedan con quien pagó). Se valida el lunes 17 con los prospectos que entran.

**Corpus DCE incorporado a la bóveda.** Los nueve documentos del programa Dirección Comercial Externa vivían solo como `.docx` en `~/Downloads` y dentro del proyecto de claude.ai — invisibles para cualquier agente. Convertidos a markdown en `00-AGC-Partners/05-Comercial-Adquisicion/DCE-Programa/` con índice: branding, avatar, oferta espejo, playbook de marketing, arquitectura BOS, manual de onboarding, contrato, propuesta vigente y tarifario preferencial. `direccion-ventas`, `direccion-marketing` y `onboarding-cliente` ya apuntan ahí.

Detalle: las copias `_1` y `_2` de Downloads son descargas repetidas byte a byte, no versiones. La única versión real distinta es `03_Oferta_Espejo_DCE_v2.0`. Faltan los números 06 y 07, y el branding nuevo que Diego hizo en claude.ai **no está descargado** — hay que bajarlo.

**Marca v2.0 incorporada y auditoría documental hecha.** Diego pasó el Documento Maestro de Marca v2.0 y la propuesta de agosto. El v2.0 declara precedencia sobre todo otro documento, así que se cruzó contra los que ya estaban en la bóveda: `Conflictos-Documentales.md` lista 11 choques abiertos. Los caros: los códigos del tarifario apuntan a servicios distintos en dos documentos que circulan (MKT-001 es Meta en uno y Google en otro; IA-001 tiene 25% de diferencia de precio), la propuesta dice "más IVA" contra la decisión de boleta exenta, y el contrato conserva el componente variable que la decisión 6 prohíbe. `01-Branding.md` (v1.0) quedó como aviso de baja para que nadie lea reglas muertas.

Consecuencia de cartera: el piso subió a $20.000.000 mensuales. **La mayoría de los clientes actuales no lo cumple** — no obliga a soltar a nadie, pero sí cambia con qué criterio se filtran los prospectos del lunes.

**Contrato v2.0 escrito sobre la matriz de la propuesta.** `09-Contrato-v2.md`. Alcance, fases, ritmo y precios salen tal cual de la Propuesta de agosto; encima se aplicaron las correcciones obligatorias del v2.0: se eliminó el componente variable, entra el Director asignado en vez del compromiso nominal de Diego, la Curva de Dirección pasa a ser tabla contractual, plazo 3+3 con hito al día 90, precio por fase y cláusula nueva de plazos y expectativas. El contrato v1 quedó como aviso de baja.

Corrección a lo que reporté antes: **el error del IVA nunca estuvo en el contrato** — la v1 ya decía "netos, boleta exenta". Está solo en la propuesta. Sigue pendiente la confirmación del contador sobre si AGC califica como sociedad de profesionales; si no califica, todos los precios se rehacen.

Reclutamiento quedó en 3 por trimestre por instrucción expresa de Diego, aunque el v2.0 pide bajarlo a 1.

**Piso de $20M propagado y tarifario unificado.** `02-Avatar.md` (ficha y anti-avatar) y el ángulo de filtro de `04-Playbook-Marketing.md` ya dicen $20.000.000. `11-Tarifario-v2.md` retira los códigos ambiguos en vez de reasignarlos —`MKT-001..005` e `IA-001/002` quedan muertos para siempre y la familia MKT parte en 101—, porque reciclar un código es exactamente lo que creó el problema. Si un cliente llega con un documento viejo, se honra el precio que ese papel dice: la ambigüedad la creó AGC.

**Dos precios quedaron sin resolver a propósito.** `IA-101` (empleado digital adicional: $320.000 vs $400.000) e `IA-102` ($160.000 vs $150.000). Precio es nivel "Dirección decide" — no se inventa. El tarifario v2 no se entrega a un cliente hasta que Diego los fije.

**Descargas minado — 155 archivos de cliente rescatados.** 28 `.docx` convertidos a markdown dentro de `Clientes/*/07-Material-Historico/`, más un índice por cliente que lista también los `.pdf` y `.xlsx` que siguen en Descargas. Las 7 fichas enlazan a su índice.

De ahí salió `01-SOPs-Maestros/Catalogo-de-Entregables.md`: **AGC ya tenía un método repetible, disperso en Descargas y sin nombrar.** La matriz real dice tres cosas incómodas — los guiones son lo único que se entrega a los 8 clientes; **solo 2 de 8 tuvieron informe mensual** (y uno era Grupal Corp, que ya se fue); y **Óptica Ferreira, el 93% de la inversión, no tiene 360 ni Manual de Marketing y Ventas** — el cliente más grande es el peor documentado. Sweet Mayorista es el mejor documentado y sirve de molde.

**WhatsApp perdió el vínculo** ("problema de sincronización") y pide QR nuevo. Bloqueado hasta que Diego escanee — 10 segundos con el teléfono.

**Riesgo nuevo:** hay 3 PDF `CREDENCIALES OPTICA FERREIRA` sueltos en `~/Downloads`.

**Torre de Control publicada.** https://claude.ai/code/artifact/9acd9a55-701a-4352-a1e4-12da7343d753 — la interfaz que Diego pidió ver al despertar: cartera con la barra de concentración, conectores vivos y caídos, los 8 comandos, lo construido y las 5 decisiones que lo esperan. Usa su propio sistema de marca (carbón `#252526`, rojo AGC `#FC2D3C`, serif editorial), que es lo que el v2.0 exige. Para actualizarla hay que republicar el mismo archivo o pasar esa URL como `url`.

**Propuesta corregida en lo que no depende del contador.** Ya dice "tu Director asignado" en vez de comprometer a Diego nominalmente, y se le incorporó la Sección 7 que faltaba: garantía del día 30 con devolución del 100% del primer mes, los plazos honestos (30 / 45-90 / 90-180) y el traspaso completo de infraestructura — todo **antes del precio**, como manda §15.1. Era la afirmación más fuerte que tiene AGC y no estaba en el documento que el prospecto se lleva.

**Plantilla de informe mensual creada** (`04-Plantillas/Informe-Mensual-Cliente.md`) y `direccion-operaciones` ya apunta ahí. Cierra la brecha 2/8. Reglas duras que trae: el número va primero aunque el mes sea malo; la sección "qué no funcionó" nunca va vacía; y sin dato de venta no se emite recomendación de presupuesto.

**8 de 11 conflictos documentales resueltos.** Quedan: el IVA (bloqueado por el contador), reclutamiento 3 vs 1 (decisión tomada por Diego) y dos menores sin urgencia.

**El riesgo número uno se materializó a las 02:00.** Consulté la API: `1946094894848` pasó de `IN_GRACE_PERIOD` a **`UNSETTLED`** y ya no responde consultas. Saldo impago con Meta pese a tener medio de pago. Propagado al Registro Maestro, a la ficha de Ferreira, a [[riesgo-concentracion]] y a la Torre de Control.

**Primer informe de dirección real generado** con datos frescos: `06-Planeacion-y-Finanzas/informes/2026-08-17-informe-direccion.md`. Últimos 30 días — Ferreira Spa $13.635.429 (CTR 1,59% · frecuencia **5,25** · CPC $90), Sweet $1.273.585 (CTR 6,04% · CPC $27), MQF $691.514 (CTR 5,31% · CPC $49). **Fatiga creativa medible en Ferreira:** costo por clic 3,4× el de Sweet porque la misma gente ve las mismas piezas cinco veces. Es rotación de creativos, no reasignación de presupuesto — y el informe **no recomienda distribución de plata** porque no hay dato de venta de ningún cliente.

Correcciones que salieron de la API: Kristus no está bloqueado, es despliegue gradual del MCP ("Ads MCP is gradually being rolled out"). La cuenta web de Ferreira `1228089025451973` corre vacía, sin gasto en 30 días. Decohogar y Fernando Saavedra siguen con accesos activos sin ser clientes.

## Pendiente

- Fase 5: levantamiento técnico.
- El correo de las 9:00 está agendado como tarea de sesión (`cron` one-shot). **Muere si se cierra la terminal.** Respaldo: borrador en Gmail con el mismo contenido.

## Requiere decisión de Diego

1. **Rotar credenciales.** Tokens de Meta, API key de Google/Gemini y token de GoHighLevel estuvieron públicos unas horas. No gobiernan datos propios: gobiernan el presupuesto publicitario de los clientes.
2. **Verificar el medio de pago de `1946094894848`.** Cuenta principal de Óptica Ferreira, en `IN_GRACE_PERIOD`, concentra el 58% de toda la inversión administrada.
