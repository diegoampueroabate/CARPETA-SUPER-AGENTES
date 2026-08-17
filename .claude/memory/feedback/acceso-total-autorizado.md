---
name: acceso-total-autorizado
description: Diego autorizó acceso amplio a su computador, navegador, descargas y chats de WhatsApp para construir el superagente
metadata:
  type: feedback
---

Diego autorizó expresamente (2026-08-17), para este proyecto, acceso a **todo su computador**: carpetas, `~/Downloads`, Google Chrome y sus pestañas abiertas, el MCP de Playwright para navegar, y los chats de WhatsApp — en particular los que se llaman **"Dirección Comercial"** o **"DC"**, que son las conversaciones operativas con clientes.

**Why:** el cuello de botella del superagente no es la capacidad, es el contexto. La información real de AGC vive dispersa fuera de la bóveda — en Downloads, en el proyecto de claude.ai, en los chats de WhatsApp. El corpus DCE es la prueba: nueve documentos que gobiernan marca, precio y contrato estaban en `~/Downloads` como `.docx` sueltos, invisibles para cualquier agente hasta que se trajeron a la bóveda. Diego prefiere que se busque y se traiga, antes que preguntarle dónde está cada cosa.

**How to apply:** buscar en el disco antes de pedirle un archivo. Si algo parece faltar, revisar `~/Downloads` y las carpetas del Escritorio primero. Los chats de WhatsApp con "Dirección Comercial"/"DC" son fuente legítima de contexto operativo de cliente — lo que salga de ahí se escribe en la ficha del cliente en la bóveda, no se queda en la respuesta.

Límites que siguen vigentes y no los levanta esta autorización:
- **Leer es libre; actuar hacia afuera no.** No enviar mensajes a clientes, no publicar, no mover presupuesto publicitario sin confirmación explícita (`ejecuta` / `aplica` / `confirma` / `procede`). Ver [[decidir-sin-preguntar]].
- Recorrer OneDrive en masa fuerza descargas — filtrar antes. Ver [[trampas-entorno]].
- Las credenciales siguen yendo por conector, nunca leídas de archivo. Ver [[credenciales-expuestas]].
