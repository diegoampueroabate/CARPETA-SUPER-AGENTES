---
name: bitacora-loop-nocturno
description: Qué se construyó y qué se encontró en el loop de la noche del 16 al 17 de agosto de 2026
metadata:
  type: project
---

# Bitácora — noche del 16 al 17 de agosto de 2026

Las cinco fases del plan quedaron cerradas. Lo más valioso de la noche no fue lo construido: fue lo que apareció al mirar datos que nadie podía leer.

---

## Lo que espera a Diego, por orden de costo

### 1 · Regularizar el pago de Óptica Ferreira · el riesgo se materializó

A las 02:00 la cuenta `1946094894848` pasó de `IN_GRACE_PERIOD` a **`UNSETTLED`** y dejó de responder consultas de la API. El período de gracia terminó: hay saldo impago con Meta pese a tener medio de pago registrado. Es la cuenta que concentra el **58% de toda la inversión administrada**. Ayer era advertencia; hoy es deuda vencida.

### 2 · Rotar credenciales

Tokens de Meta, API key de Google/Gemini y token de GoHighLevel estuvieron públicos unas horas. Se suman dos hallazgos de la noche: **3 PDF `CREDENCIALES OPTICA FERREIRA`** sueltos en `~/Downloads`, y el **token del pixel de Sweet en texto plano** dentro de un `.docx`, que yo mismo importé por error a la bóveda antes de retirarlo. No gobiernan datos propios: gobiernan el presupuesto publicitario de los clientes.

### 3 · Facturación · ¿por dónde se factura realmente?

Verificado por conector: la cuenta de WASABIL de **AMPUERO ABATE CONSULTING GROUP LIMITADA** (RUT 78.468.795-3) tiene `can_issue: false`, `configured: false`, sin certificado, sin folios y **cero documentos en el historial completo**. El conector devuelve vacío en vez de error, así que cualquier informe construido sobre él falla en silencio.

Y en las rendiciones de Ferreira aparecen dos cosas:

- Una línea de **$180.000 mensuales rotulada literalmente "SIN BOLETA"** — $2,16 M al año en un solo cliente, con el régimen de IVA aún sin confirmar.
- **119 videos entregados al mes contra los 8 que incluye el programa.** La planilla los asume como "servicio bonificado" a un valor referencial declarado de $12.000 por video: **entre $1,0 y $1,4 millones de trabajo regalado cada mes**, casi el fee completo.

Detalle en `06-Planeacion-y-Finanzas/Estado-de-la-facturacion.md`.

### 4 · Confirmar el régimen tributario con el contador, por escrito

La entidad es una **Limitada**, no una sociedad de profesionales por defecto. De eso depende la exención de IVA de la decisión 5 del v2.0. **Bloquea corregir la propuesta**, que hoy dice "más IVA" — $226.100/mes de diferencia solo en Fase 1. Si no califica, todos los precios se rehacen. Contador primero, propuesta después.

### 5 · Escanear el QR de WhatsApp

La sesión perdió el vínculo por un problema de sincronización. Hasta que se reenlace no se pueden leer los chats "DC". Diez segundos con el teléfono.

### 6 · Aprobar rotación de creativos en Ferreira

Nivel *Dirección aprueba*: la propuesta se arma sin tocar nada. Fatiga medible en `1049367834100232` — frecuencia **5,25** y CTR **1,59%** en 30 días, contra 6,04% de Sweet y 5,31% de MQF. Costo por clic **3,4×** el de Sweet. No es presupuesto ni audiencia: la misma gente ve las mismas piezas cinco veces.

### 7 · Decisiones menores abiertas

- Reclutamiento: quedó en 3 procesos por trimestre por instrucción expresa; el v2.0 pide 1. Con 4 clientes no se nota, con 10 sí.
- Los repos están commiteados **en local, sin push**. Subir después de la filtración es decisión de Diego.

---

## El hallazgo central de la noche

**El dato de venta no existe.** Tres clientes lo tienen marcado como punto crítico en su propio 360: Sweet ("el 90%+ de las ventas no existe en el sistema"), Odawe ("las 300+ ventas por live NO se ingresan al sistema"), y Ferreira, cuyo cruce de marzo se armó a mano en una planilla — por eso hay un mes y no seis.

Es la característica del segmento: mayoristas que venden por live, cierran por WhatsApp y cobran por transferencia. El ciclo ocurre fuera de todo sistema que registre. Consecuencia: **el CRM no es un componente del paquete, es el primer entregable** — sin él no se puede demostrar que el trabajo funciona. Y es el argumento de venta más fuerte que AGC tiene sin usar. Ver `02-Base-Conocimiento/El-dato-de-venta-no-existe.md`.

AGC tiene el mismo problema: cero documentos en WASABIL, $180.000/mes sin boleta.

## Corrección del piso — mi afirmación era falsa

Escribí que "la mayoría de los clientes no cumple el piso de $20M". Lo afirmé sin dato. Los 360 dicen: Ferreira $95,7M medido · Sweet $24-40M · MQFJOYAS $30-35M · Kristus $30-35M · Carlitos $120-130M · Odawe $20-70M por live. **Los cuatro que pagan lo superan, y los dos cerrados también.** El piso no amenaza la cartera: describe el perfil que AGC ya atiende.

## Plantillas del método, extraídas de lo entregado

Sweet y Odawe tienen el **mismo** Manual de Ventas y Marketing con los nombres cambiados: misma estructura, mismo recorrido de seis pasos, y en ambos el paso 4 —esperar respuesta— es donde se cae la venta. `04-Plantillas/Manual-Ventas-y-Marketing.md` y `04-Plantillas/360-del-Negocio.md` salen de ahí, no de una invención.

Nota técnica: los PDF se leen con **PyMuPDF** (`import pymupdf`), que está disponible. Extrae texto sin gastar contexto en imágenes — así se abrieron los ~90 PDF de cliente de Descargas.

## Lo que se construyó

**Fase 1 · fuente de verdad.** Registro Maestro reescrito contra la API: 20 cuentas cruzadas, cartera en 4 que pagan + 2 sin cobro. Se eliminaron dos `account_id` inexistentes que hacían fallar consultas en silencio. Las 9 fichas con frontmatter y alias de Obsidian para que los wikilinks resuelvan.

**Fase 2 · las cinco direcciones** en `.claude/skills/`: marketing, ventas, operaciones, rrhh, finanzas. Cada una arranca leyendo el Registro Maestro, respeta "por defecto solo recomendar" y escribe en la bóveda. Los 240+ skills existentes se referencian desde su repo — no se copian.

**Fase 3 · memoria persistente** en `.claude/memory/`, indexada en MEMORY.md.

**Fase 4 · `/onboarding-cliente`.** Nombre canónico confirmado antes de crear nada, Registro Maestro antes que la carpeta, `meta_account_ids: []` vacío en vez de inventado, y la secuencia para el prospecto sin cuenta publicitaria — BM a nombre del cliente, no de AGC.

**Fase 5 · levantamiento técnico.** El hallazgo fue que nada estaba versionado: la bóveda con 24 cambios sin commitear y el orquestador **sin git en absoluto**. Ambos commiteados.

**Corpus comercial en la bóveda.** Los nueve documentos del programa vivían como `.docx` en Descargas, invisibles para cualquier agente. Convertidos a `05-Comercial-Adquisicion/DCE-Programa/`, con la **Marca v2.0** declarada de máxima precedencia y la v1.0 retirada a aviso de baja.

**8 de 11 conflictos documentales resueltos.** Contrato v2 sin componente variable, con Director asignado y la Curva de Dirección como tabla contractual, plazo 3+3. Tarifario v2 con los códigos ambiguos **retirados, no reasignados** (`MKT-001..005` e `IA-001/002` quedan muertos; la familia MKT parte en 101). Propuesta con garantía del día 30 y plazos honestos, antes del precio. Piso de entrada a **$20.000.000** propagado al avatar y al playbook.

**155 archivos de cliente rescatados de Descargas**, 28 convertidos a markdown en `Clientes/*/07-Material-Historico/` con índice por cliente. De ahí salió `01-SOPs-Maestros/Catalogo-de-Entregables.md`: AGC ya tenía un método repetible, sin nombrar. La matriz dice que los guiones son lo único que se entrega a los 8 clientes, que **solo 2 de 8 tuvieron informe mensual**, y que **Ferreira es el peor documentado** de la cartera.

**Plantilla de informe mensual** (`04-Plantillas/Informe-Mensual-Cliente.md`) y el **primer informe real** con datos de la API (`06-Planeacion-y-Finanzas/informes/2026-08-17-informe-direccion.md`).

**Los dos únicos cruces de gasto contra venta que existen**, extraídos de `.xlsx` ilegibles:

- **Kristus** — gira norte: venta $11.757.999 · pauta $760.323 · ROAS **15,46×** · margen neto **12,6%**. Su conector está deshabilitado, así que ese archivo es su única fuente de datos.
- **Ferreira** — marzo: venta $95.780.000 · pauta $10.123.080 · ROAS **9,46×** sobre 59 operativos.

De cruzarlos salió `02-Base-Conocimiento/ROAS-no-es-rentabilidad.md`: un ROAS de 15,46× dejó 12,6% de margen neto, porque el ROAS descuenta solo la pauta. **Un informe puede reportar ROAS; no puede llamarlo rentabilidad.** Ferreira corre a 9,46× y no se conoce ni su margen ni el costo de sus operativos.

**Torre de Control publicada:** https://claude.ai/code/artifact/9acd9a55-701a-4352-a1e4-12da7343d753 — para actualizarla, republicar el mismo archivo o pasar esa URL como `url`.

---

## Correcciones a lo que reporté antes

- El error del IVA **nunca estuvo en el contrato**; la v1 ya decía "netos, boleta exenta". Está solo en la propuesta.
- El fee de Ferreira es **$1.180.000**, no $710.000: había leído solo las primeras filas de la planilla. Está en línea con los $1.190.000 del programa.
- **Kristus no está bloqueado por Meta** — es despliegue gradual del MCP, puede habilitarse solo.

## Pendiente sin bloqueo

- La cuenta web de Ferreira `1228089025451973` corre vacía: sin gasto en 30 días.
- Decohogar y Fernando Saavedra mantienen accesos activos sin ser clientes.
- Faltan los documentos 06 y 07 de la serie DCE; no existen en el disco.
- Ferreira sigue sin 360 del Negocio ni Manual de Marketing y Ventas. **No los escribí**: requieren margen, equipo, locales y proceso de venta que no tengo. Escribirlos con lo disponible sería fabricar un documento para el cliente más grande.
- El correo de las 9:04 está agendado como tarea de sesión. **Muere si se cierra la terminal.** Respaldo: borrador en Gmail.
