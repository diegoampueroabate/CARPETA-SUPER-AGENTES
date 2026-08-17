---
name: mapa-ecosistema
description: Qué contiene cada carpeta del Escritorio y dónde vive cada tipo de trabajo
metadata:
  type: reference
---

Cada agente es un repo privado independiente en `github.com/diegoampueroabate`, en carpetas hermanas del Escritorio:

| Carpeta | Contenido |
|---|---|
| `AGENTE DE PROCESO` | Bóveda Obsidian — Registro Maestro, SOPs, fichas de cliente, ~30 skills |
| `AGENTE ADS MANAGER` | 20 skills de Meta + `proyectos/` con material real (11,2 GB) |
| `AGENTE COPY WRITTER` | 47 skills de contenido |
| `AGENTE RECURSOS HUMANO` | 146 skills en `hr-skills-main/` |
| `AGENTE PARA DISEÑOS IA` | Estilos de ads, `nano-banana-pro` |
| `AGENTE GHL` | `ghl-mcp/`, `subcuentas/`, workflows |
| `finanzacrm` | Next.js + Supabase — único proyecto con código y toolchain |
| `CARPETA SUPER AGENTES` | Orquestador: CLAUDE.md, `.claude/skills/`, `.claude/memory/` |

**Por qué importa:** son ~240 skills. Copiarlos al orquestador los hace divergir en un mes.

**Cómo aplicarlo:** se referencian desde su repo de origen. Convención uniforme: `nombre-del-skill/nombre-del-skill.md` + `casos-de-uso.txt`, en español con guiones. Ver [[trampas-entorno]] antes de recorrer carpetas en masa.
