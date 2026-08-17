---
name: credenciales-expuestas
description: Inventario exacto de las 26 credenciales que están en el historial de git y hay que rotar
metadata:
  type: project
---

# 26 credenciales en el historial de git

Auditado el 2026-08-17 sobre los 8 repos. **Están en el historial desde el commit inicial**, y los repos estuvieron públicos unas horas antes de volverse privados.

## Qué hay que rotar, exactamente

| Archivo | Credencial | Cuántas |
|---|---|:-:|
| `AGENTE ADS MANAGER/AccessMD/meta_tokens.md` | Meta | 12 |
| `AGENTE ADS MANAGER/.claude/settings.json` | Meta | 5 |
| `AGENTE ADS MANAGER/.claude/.claude/settings.json` | Meta | 2 |
| `AGENTE ADS MANAGER/AccessMD/gemini_api.md` | Google/Gemini | 1 |
| `AGENTE ADS MANAGER/CLAUDE.md` línea 217 | Google/Gemini | 1 |
| `AGENTE GHL/KEYS.md` | GoHighLevel | 3 |
| `AGENTE GHL/.claude/settings.local.json` | GoHighLevel | 2 |
| `AGENTE GHL/.claude/settings.json` | GoHighLevel | 1 |

**19 de Meta · 2 de Google/Gemini · 6 de GoHighLevel.**

Fuera de git, en `~/Downloads`: 3 PDF `CREDENCIALES OPTICA FERREIRA` y el token del pixel de Sweet dentro de `PIXEL Y TOKEN SWEET.docx`.

## Lo que se hizo y lo que NO alcanza

Hecho: los archivos salieron del control de versiones (`git rm --cached`, siguen en disco) y el `.gitignore` de cada repo los cubre. La key de Gemini se retiró del `CLAUDE.md` de ADS MANAGER y se reemplazó por `$GEMINI_API_KEY`.

**Eso detiene la exposición futura, no la pasada.** Retirar un secreto del árbol de trabajo no lo borra del historial: cualquiera con una copia del repo lo tiene. Borrarlo de verdad exige reescribir el historial (`filter-repo` o similar) y forzar push, y eso es decisión de Diego — no se hace solo.

**La única acción que cierra el riesgo es rotar las 26.** Hasta entonces siguen siendo válidas.

## Por qué esto importa más de lo que parece

Estos tokens no gobiernan datos propios: gobiernan el **presupuesto publicitario de los clientes**. Un token de Meta con permisos de escritura permite crear campañas y gastar plata en las cuentas de Óptica Ferreira, Sweet, MQFJOYAS y Kristus.

## La regla que evita que vuelva a pasar

`CLAUDE.md` · sección Credenciales: van por **conector autenticado** (`mcp__claude_ai_FACEBOOK__*`, Drive, Gmail, Supabase) o por **variable de entorno**. Nunca literales en archivo. `AccessMD/` y `KEYS.md` están en `.gitignore` de sus repos.

El escaneo previo al commit es parte del procedimiento, no un extra: en esta misma noche detectó un token del pixel de Sweet que yo había importado por error a la bóveda. Ver [[bitacora-loop-nocturno]].
