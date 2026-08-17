---
name: credenciales-expuestas
description: Tokens de Meta, Google y GoHighLevel estuvieron públicos el 16-ago-2026 y siguen sin rotar
metadata:
  type: project
---

El 16-ago-2026, ocho repositorios de AGC estuvieron públicos unas horas con credenciales vivas dentro: usuarios de sistema de Meta, app secret, token CAPI, API key de Google/Gemini y token de GoHighLevel. Los repos volvieron a privado el mismo día. **La rotación sigue pendiente de Diego.**

**Por qué importa:** esos tokens no gobiernan datos propios de Diego — gobiernan el presupuesto publicitario de sus clientes. Volver el repo a privado no invalida lo que ya se copió.

**Cómo aplicarlo:** la causa raíz no era el repo público sino el token en archivo. Meta se consulta por el conector `mcp__claude_ai_FACEBOOK__*`, que está autenticado y no necesita credencial local. Ningún token se escribe en archivo: variable de entorno o nada. `AccessMD/` y `KEYS.md` van en `.gitignore`.
