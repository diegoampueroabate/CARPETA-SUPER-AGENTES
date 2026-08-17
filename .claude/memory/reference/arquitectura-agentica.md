---
name: arquitectura-agentica
description: Qué tomar y qué descartar de los diagramas de Structure Webworks que Diego usa como referencia
metadata:
  type: reference
---

Diego sigue a **Structure Webworks** (TikTok) y usa sus diagramas de arquitectura agéntica como norte. Son la referencia visual que tenía en mente cuando pidió el superagente.

## Lo que sí se adoptó

**El Loop.** Marketing → Ventas → Operaciones → Seguimiento → Finanzas → feedback → decisiones del mes siguiente. Es el aporte real de esos diagramas: las cinco direcciones existían como piezas sueltas y no como ciclo que se cierra. El feedback de finanzas es lo que hace que el mes siguiente se decida con datos y no con sensaciones.

**Los tres niveles de autonomía.** De su "Monday Decision Brief": `HUMAN-LED` · `HUMAN-ASSISTED` · `FULLY AUTONOMOUS`. Encaja exacto con la regla heredada de ADS MANAGER ("por defecto, solo recomendar") y le da vocabulario: no todo requiere el mismo grado de intervención de Dirección.

**Las compuertas de aprobación humana.** Trato de alto valor, precio o descuento, excepción contractual, cambio de estrategia, escalamiento. Esas cinco siempre pasan por Diego.

**Una página cada mañana.** El informe de dirección: no un dashboard que hay que ir a mirar, sino un documento que llega. Ver el skill `informe-direccion`.

**La capa de conocimiento como sistema de archivos.** `/context`, `/skills`, `/agents`, `/approvals`, `/reports`. AGC ya lo tiene: la bóveda es `/context`, los ~240 skills de los repos son `/skills`, `.claude/skills/` son las direcciones y `.claude/memory/` es la memoria persistente. No hace falta construirlo de nuevo.

## Lo que NO se adopta, y por qué

Varios diagramas muestran **Redis, BullMQ, NGINX como load balancer, Prometheus, Grafana, Logstash, Elasticsearch, Kibana, Temporal, LangGraph, Clerk, réplica de PostgreSQL**.

Eso es la infraestructura de un SaaS con miles de usuarios concurrentes. AGC tiene **4 clientes que pagan**. Un balanceador de carga para cuatro cuentas es costo puro, y cada pieza de esas es una cosa más que se cae a las 3 de la mañana. Es contenido hecho para verse impresionante en un video, no para operar una consultora chilena.

La regla: **la bóveda de markdown y los conectores ya autenticados hacen el mismo trabajo, sin servidores que mantener.** Si algún día AGC tiene 40 clientes y la bóveda no da abasto, se reevalúa — hoy no.

Tampoco se adoptan las cifras de agentes ("133 agentes", "Finance: 21 agentes"). Contar agentes no es una métrica: un agente que no tiene datos reales que leer no hace nada, por muchos que sean. El cuello de botella de AGC nunca fue cantidad de agentes — fue que la información vivía fuera de la bóveda. Ver [[corpus-dce]].

## La diferencia de fondo

Esos diagramas asumen que los datos ya están conectados y limpios. En AGC no lo estaban: había tres listados de clientes que no coincidían y dos `account_id` inexistentes fallando en silencio. Por eso la Fase 1 fue reconciliar la fuente de verdad y no dibujar agentes. Ver [[cartera-reconciliada]].
