# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Qué es este workspace

Orquestador del superagente de **AGC Partners** (agencia chilena de dirección comercial externa: 4 clientes que pagan, 2 sin cobro). No contiene lógica propia: enruta trabajo hacia agentes especializados que viven en carpetas hermanas del Escritorio, y coordina el estado a través de una bóveda markdown compartida.

Todo se escribe en **español**: nombres de carpetas, skills, notas de la bóveda y respuestas al usuario.

**Este archivo nunca supera las 200 líneas.** Orden permanente de Dirección. Se carga en cada sesión y en cada subagente, así que cada línea se paga muchas veces. Lo que no cabe baja a `.claude/skills/` o a `.claude/memory/`, que se cargan solo cuando hacen falta.

## Ruteo por área

No resuelvas directo lo que tiene dirección. Invoca el skill y deja que él decida el especialista.

| Si el trabajo es de… | Invoca |
|---|---|
| Meta Ads, copy, creativos, contenido | `direccion-marketing` |
| Prospectos, propuestas, pipeline GHL | `direccion-ventas` |
| SOPs, incorporación, informes, bóveda | `direccion-operaciones` |
| Cargos, selección, delegación | `direccion-rrhh` |
| Rentabilidad, SII, riesgo de cartera | `direccion-finanzas` |

Cliente nuevo (o uno que se atiende sin ficha): `onboarding-cliente`. Da de alta en el Registro Maestro primero, crea la carpeta, declara los vacíos bloqueantes el día 1 y reparte a las direcciones.

Estado de todo junto, brief del lunes, cierre de mes: `informe-direccion`. Cierra el ciclo — las direcciones producen trabajo, el informe lo convierte en decisiones.

## Los tres niveles de autonomía

Toda salida se clasifica en uno. **Nunca subas de nivel por cuenta propia.**

| Nivel | Qué significa |
|---|---|
| **Dirección decide** | Precio, descuentos, excepciones de contrato, aceptar o rechazar un prospecto, cambio de estrategia, escalamiento. Nada se ejecuta antes |
| **Dirección aprueba** | Viene resuelto y propuesto; falta el visto bueno |
| **Ya está hecho** | Se ejecutó y solo se informa: bóveda, informes, documentación, seguimiento |

Mover una decisión de "decide" a "aprueba" es el trabajo real del sistema. No reemplaza el criterio de Diego: le llega el material terminado hasta donde su criterio empieza.

Los subagentes no se pasan mensajes: cada uno lee la ficha del cliente y escribe su resultado en la bóveda. Ese es el canal.

`.claude/memory/MEMORY.md` es el índice de memoria persistente. Léelo al empezar; el detalle está en los archivos que indexa.

## Alcance de acceso

Dirección autorizó acceso amplio: disco completo, `~/Downloads`, Chrome y sus pestañas (MCP Playwright), y los chats de WhatsApp llamados "Dirección Comercial" o "DC". Busca en el disco antes de pedirle un archivo — el corpus comercial completo estaba en Descargas, invisible para los agentes.

**Leer es libre; actuar hacia afuera no.** No se envía nada a un cliente, no se publica y no se mueve presupuesto sin confirmación explícita.

## Fuente de verdad comercial

`00-AGC-Partners/05-Comercial-Adquisicion/DCE-Programa/`. `01-Marca-v2.md` tiene precedencia sobre contrato, propuesta y playbook. Antes de cotizar o firmar, leer `Conflictos-Documentales.md`: hay contradicciones abiertas entre documentos que circulan. Piso de entrada vigente: **$20.000.000** mensuales.

## El ecosistema

Cada agente es un repositorio privado independiente en `github.com/diegoampueroabate`. Se referencian, no se copian — duplicar los skills los hace divergir.

| Carpeta (en `Escritorio/`) | Rol | Contenido |
|---|---|---|
| `AGENTE DE PROCESO` | **Cerebro compartido** | Registro Maestro, SOPs, fichas de cliente, ~30 skills operativos |
| `AGENTE ADS MANAGER` | Meta Ads | 20 skills + `proyectos/` con material real por cliente |
| `AGENTE COPY WRITTER` | Contenido y copy | 47 skills |
| `AGENTE RECURSOS HUMANO` | Reclutamiento | 146 skills en `hr-skills-main/` |
| `AGENTE PARA DISEÑOS IA` | Creativos e imagen | Estilos de ads, `nano-banana-pro` |
| `AGENTE GHL` | CRM / automatización | `ghl-mcp/`, `subcuentas/`, workflows |
| `RECURSOS IMAGENES IA` | Referencia | Guías de prompting en PDF |
| `finanzacrm` | Aplicación real (Next.js) | CRM financiero — único proyecto con código |

## La bóveda es el estado compartido

`AGENTE DE PROCESO` es una bóveda Obsidian: markdown plano, leíble directo del disco. No requiere plugin ni MCP.

**Regla de oro** (de `00-AGC-Partners/01-SOPs-Maestros/SOP-Fuente-de-Verdad.md`): `00-Registro-Maestro-Clientes.md` es la única fuente de la identidad de cada cliente. Un cambio se hace **primero ahí** y luego se propaga. Un cliente = un nombre canónico, siempre el mismo en carpetas, en ADS MANAGER y en finanzacrm.

Los subagentes no se pasan mensajes entre sí: cada uno lee la ficha del cliente y escribe su resultado en la bóveda. Ese es el canal.

**Reconciliado el 2026-08-16.** Convivían tres listados que no coincidían (7 en el Registro, 11 en ADS MANAGER, 20 cuentas reales en Meta) y dos `account_id` en uso activo no existían: las consultas fallaban en silencio. Por eso ningún `account_id` se usa de memoria ni de un documento antiguo — se verifica contra `ads_get_ad_accounts` primero.

**Riesgo abierto:** el 93% de la inversión administrada es Óptica Ferreira, y su cuenta principal `1946094894848` pasó a `UNSETTLED` el 2026-08-17 — saldo impago con Meta, ya no responde consultas. Se reporta en cada revisión hasta que se cierre, **verificando el estado contra la API**: cambió de un día para otro.

**El dato de venta no existe en el segmento.** Tres clientes lo tienen marcado como punto crítico en su propio 360: las ventas por live no se registran en ningún sistema. Ningún informe puede cruzar gasto contra venta hasta que el registro exista, y pedírselo al cliente no sirve porque tampoco lo tiene. Ver `02-Base-Conocimiento/El-dato-de-venta-no-existe.md`.

## Convención de skills

Uniforme en los cuatro repos de skills, ~240 en total:

```
nombre-del-skill/
  nombre-del-skill.md    ← el prompt/instrucción
  casos-de-uso.txt       ← cuándo aplica
```

Al crear uno nuevo, seguir exactamente ese patrón y nombrarlo en español con guiones.

## Credenciales: por conector, nunca en archivo

Los tokens de Meta estuvieron incrustados en `AGENTE ADS MANAGER/AccessMD/meta_tokens.md`, en `.claude/settings.json` y en scripts `.py` de `proyectos/**/_build/`. Ese patrón queda **prohibido**.

Meta se consulta por el conector `mcp__claude_ai_FACEBOOK__*` (insights, campañas, ad sets, creativos, audiencias, catálogos), que está autenticado y no necesita tokens locales. Igual para Drive, Gmail, Calendar, Supabase y facturación SII (WASABIL).

Si un script necesita una credencial: variable de entorno, nunca literal. `AccessMD/` y `KEYS.md` van en `.gitignore`.

## Comportamiento heredado que se respeta

`AGENTE ADS MANAGER/CLAUDE.md` define **"por defecto: solo recomendar"** — analizar, diagnosticar, proponer, y esperar confirmación explícita (`ejecuta`, `aplica`, `confirma`, `procede`) antes de tocar una campaña. El orquestador no puede saltarse esa confirmación: mueve presupuesto publicitario real de clientes.

También define modo compacto obligatorio (máx. 8 líneas por respuesta) y una tabla de Fast Path con umbrales de diagnóstico ya calibrados — usarla antes de razonar desde cero.

## Comandos

Solo `finanzacrm` tiene toolchain. Desde su carpeta:

```bash
npm run dev      # Next.js con turbopack
npm run build
npm run lint
npm start
```

Stack: Next.js + Supabase (`@supabase/ssr`), Tailwind, zustand, zod, recharts. `src/` está dividido en `app/`, `features/`, `lib/`, `shared/`.

Su `.mcp.json` levanta `next-devtools`, `playwright` y el MCP de Supabase (project ref `jmhlfzmlbykokblkvqyr`).

**Ojo:** el `CLAUDE.md` de `finanzacrm` describe "SaaS Factory V4", no un CRM financiero — quedó copiado de `saas-factory-setup-main`. No tomarlo como fuente de verdad de ese proyecto.

Los demás repos son colecciones de markdown: no hay build, lint ni tests.

## Particularidades del entorno

- **OneDrive con archivos en la nube.** Buena parte del Escritorio son marcadores, no archivos locales. Leerlos fuerza la descarga — `AGENTE ADS MANAGER` son 11,2 GB de video. Antes de recorrer en masa, filtrar por atributo o excluir media.
- **PowerShell 5.1 lee scripts como ANSI.** Un `.ps1` escrito en UTF-8 con `ñ` o acentos falla al parsear. Escribir scripts solo en ASCII y resolver rutas con comodín (`'AGENTE PARA DISE*OS IA'`).
- Nombres de carpeta con espacios y acentos: siempre `-LiteralPath` y comillas.
- `git ls-files` escapa rutas no-ASCII; usar `-c core.quotepath=false` al comparar contra el disco.
