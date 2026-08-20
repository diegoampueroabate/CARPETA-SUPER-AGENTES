# Superagente de AGC Partners — orquestador

Este repositorio **no contiene el conocimiento del negocio**. Es la capa de ruteo: siete comandos que deciden qué especialista trabaja y con qué reglas.

El conocimiento vive en un repositorio hermano, **`AGENTE-DE-PROCESO`**, que es una bóveda de Obsidian con 266 archivos markdown. Los dos son inseparables: sin la bóveda, cada skill de acá apunta a archivos que no existen.

## Los dos repositorios, y por qué son dos

| | Qué es | Cuántos archivos |
|---|---|---|
| **`carpeta-superagentes`** (este) | Orquestador, 7 skills, memoria persistente | 25 |
| **`AGENTE-DE-PROCESO`** | La bóveda: Registro Maestro, fichas de cliente, SOPs, corpus comercial | 266 |

Se clonan **uno al lado del otro**, en la misma carpeta padre. Las rutas de los skills asumen esa disposición:

```
Escritorio/
├── CARPETA SUPER AGENTES/     ← este repo
└── AGENTE DE PROCESO/         ← la bóveda
```

Hay cinco repositorios más (`AGENTE ADS MANAGER`, `AGENTE COPY WRITTER`, `AGENTE RECURSOS HUMANO`, `AGENTE PARA DISEÑOS IA`, `AGENTE GHL`) con ~240 skills de dominio. **Se referencian, no se copian**: duplicarlos los hace divergir en un mes.

> ⚠️ `AGENTE ADS MANAGER` y `AGENTE GHL` tienen credenciales en su historial de git, pendientes de rotación. No los hagas públicos.

## Cómo está armado

```
CLAUDE.md                    El orquestador. Se carga en cada sesión: nunca supera 200 líneas
.claude/
  skills/                    7 comandos, invocables con /nombre
    direccion-marketing/     Meta Ads, copy, creativos
    direccion-ventas/        Pipeline GHL, propuestas, cierre
    direccion-operaciones/   SOPs, reportería, integridad de la bóveda
    direccion-rrhh/          Cargos, selección, delegación
    direccion-finanzas/      Rentabilidad, SII, riesgo de cartera
    onboarding-cliente/      Alta de cliente de punta a punta
    informe-direccion/       Estado de todo y decisiones pendientes
  memory/                    Memoria persistente entre sesiones
    MEMORY.md                Índice. Lo único que se carga siempre
    user/ feedback/ project/ reference/
```

Cada skill lleva frontmatter YAML con `context: fork` — corre aislado — y `allowed-tools` acotado.

## Las tres reglas que gobiernan todo

**1 · Una sola fuente de verdad.** `AGENTE-DE-PROCESO/00-AGC-Partners/00-Registro-Maestro-Clientes.md` es la única fuente de la identidad de cada cliente. Un cambio se hace **primero ahí** y después se propaga.

Convivieron tres listados que no coincidían (7 en el Registro, 11 en otro repo, 20 cuentas reales en Meta) y **dos `account_id` en uso activo no existían**: las consultas fallaban en silencio, sin error. Por eso ningún identificador se usa de memoria — se verifica contra la API primero.

**2 · Tres niveles de autonomía.** Toda salida se clasifica en uno, y nunca se sube de nivel por cuenta propia:

- **Dirección decide** — precio, descuentos, excepciones de contrato, aceptar o rechazar un prospecto. Nada se ejecuta antes.
- **Dirección aprueba** — viene resuelto y propuesto; falta el visto bueno.
- **Ya está hecho** — se ejecutó y solo se informa.

**3 · Las credenciales van por conector, nunca en archivo.** Meta, Drive, Gmail, Calendar, Supabase y facturación SII se consultan por conectores ya autenticados. Si un script necesita una credencial, va en variable de entorno.

## Los subagentes no se pasan mensajes

Cada uno lee la ficha del cliente y **escribe su resultado en la bóveda**. Ese es el canal, y es deliberado: no hay bus de mensajes, no hay cola en memoria, y el estado sobrevive a que se cierre la sesión.

## Para conectarlo a otro sistema

Lo que un desarrollador probablemente quiere:

- **Leer el estado** → parsear el frontmatter YAML de las fichas en `AGENTE-DE-PROCESO/Clientes/Cliente-0X-*/00-Ficha-Cliente.md`. Hay un parser de referencia en `finanzacrm/scripts/lib/boveda.mjs`.
- **Disparar un agente** → invocar `claude -p` con el prompt por stdin y `cwd` en la raíz de este repo, para que cargue `CLAUDE.md` y los skills. Hay un worker de referencia en `finanzacrm/scripts/worker-agentes.mjs`.
- **Escribir resultados** → el agente escribe archivos; quien lo invocó los lee y persiste. **El agente nunca habla con una base de datos**: así ninguna credencial entra a su contexto.

Hay un CRM en curso (`finanzacrm`, Next.js + Supabase) que consume todo esto. Su plan y su modelo de datos están en las migraciones de `supabase/migrations/`.

## Advertencias del entorno

- **OneDrive con archivos en la nube.** Buena parte del Escritorio son marcadores, no archivos locales. Leerlos fuerza la descarga: `AGENTE ADS MANAGER` son 11,2 GB de video. Filtrar antes de recorrer en masa.
- **PowerShell 5.1 lee los `.ps1` como ANSI.** Un script en UTF-8 con `ñ` o acentos falla al parsear. Escribir scripts solo en ASCII.
- Nombres de carpeta con espacios y acentos: siempre `-LiteralPath` y comillas.
- `git ls-files` escapa rutas no-ASCII; usar `-c core.quotepath=false` al comparar contra el disco.

## Confidencialidad

Este repositorio contiene facturación de clientes reales, precios, términos de contrato y notas internas de la operación. **Mantener privado.** El acceso se da por invitación de colaborador, no publicándolo.
