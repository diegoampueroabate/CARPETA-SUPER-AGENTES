---
name: claude-md-200-lineas
description: Orden permanente de Diego — CLAUDE.md nunca supera las 200 líneas
metadata:
  type: feedback
---

`CLAUDE.md` se mantiene en 200 líneas o menos. Diego lo dio como orden que no se rompe nunca.

**Por qué:** ese archivo se carga en contexto en cada sesión y en cada subagente. Cada línea se paga muchas veces. Un CLAUDE.md que crece sin control es la forma más cara de guardar información que casi nunca se usa.

**Cómo aplicarlo:** verifica el conteo antes de cerrar cualquier edición del archivo. Lo que no cabe no se borra: baja a un skill (`.claude/skills/`) o a la memoria, que se cargan solo cuando hacen falta. Ese es el mismo principio de progressive disclosure que sostiene toda la arquitectura.
