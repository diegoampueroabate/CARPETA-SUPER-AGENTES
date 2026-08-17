---
name: onboarding-cliente
description: Incorpora un cliente nuevo a AGC Partners de punta a punta — alta en el Registro Maestro, carpeta en la bóveda, vacíos bloqueantes, y delegación a las direcciones. Actívalo cuando entra un prospecto cerrado o hay que formalizar a alguien que ya se está atendiendo sin ficha.
user-invocable: true
context: fork
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Incorporación de cliente

Hoy este tramo consume 5-7 días de Dirección y es el cuello de botella nombrado en el diagnóstico. El objetivo de este comando es que el día 1 termine con el cliente existiendo de verdad en el sistema y con los vacíos ya declarados — no con una carpeta vacía y una promesa.

## Lo que necesitas antes de escribir nada

Cinco datos. Si falta alguno, pregúntalo; no lo inventes ni lo dejes en `[__]` silencioso.

1. **Nombre canónico** — como se llamará en todos lados, para siempre. Mayúsculas y forma exactas.
2. **Contacto principal** — nombre, cargo, canal.
3. **Modalidad** — `paga` · `sin cobro` · `cerrado`.
4. **Servicio contratado** — adquisición / operaciones / setup.
5. **Fecha de inicio.**

El nombre canónico es la decisión irreversible del proceso: renombrarlo después obliga a tocar la bóveda, ADS MANAGER y finanzacrm a la vez. Confírmalo con Diego textualmente antes de crear la carpeta.

## Secuencia

### 1. Registro Maestro primero

Escribe la fila en `AGENTE DE PROCESO/00-AGC-Partners/00-Registro-Maestro-Clientes.md` **antes** de crear la carpeta. Es la fuente de verdad; todo lo demás es propagación. Sube el contador del frontmatter (`clientes_pagados` / `clientes_sin_cobro`) y `ultima_actualizacion`.

### 2. Carpeta

Copia `Clientes/_PLANTILLA-CLIENTE` a `Clientes/Cliente-NN-Nombre-Canonico` con el siguiente NN libre. Rellena `00-Ficha-Cliente.md` con frontmatter YAML igual al de las fichas existentes:

```yaml
---
nombre_canonico: NOMBRE EXACTO
modalidad: paga
meta_account_ids: []
gasto_90d_clp: 0
---
```

`meta_account_ids: []` vacío es un estado válido y honesto. **No inventes ni copies un ID de un documento antiguo.** Cuando exista la cuenta, se verifica contra `ads_get_ad_accounts` y recién ahí se escribe. Dos IDs inexistentes vivieron meses en producción haciendo fallar consultas en silencio: ese es el precio de rellenar el campo por completarlo.

### 3. Vacíos bloqueantes — el día 1, no en tres semanas

Emite explícitamente qué falta para poder trabajar. Los cuatro que siempre faltan:

| Dato | Sin él no se puede |
|---|---|
| Ticket promedio | calcular si la campaña es rentable |
| Margen por venta | saber cuánto se puede pagar por lead |
| Tasa de cierre | traducir conversaciones a plata |
| Estado de accesos | ejecutar nada |

Escríbelos en `01-Alcance-y-Contrato/Objetivos-y-KPIs.md` como preguntas abiertas con responsable y fecha. Un vacío escrito se cobra; uno mental se olvida.

### 4. Caso sin cuenta publicitaria

Un prospecto recién cerrado normalmente **no tiene** Business Manager ni cuenta de anuncios. No es un bloqueo del onboarding — es su propia tarea, y va en `02-Accesos-y-Activos/Accesos.md` con este orden, porque cada paso depende del anterior:

1. Página de Facebook e Instagram profesional vinculada.
2. Business Manager a nombre del **cliente**, no de AGC. AGC entra como socio.
3. Cuenta publicitaria dentro de ese BM, con medio de pago del cliente cargado.
4. Pixel/dataset instalado y verificado con tráfico real antes de gastar.
5. AGC solicita acceso de socio y confirma que puede leer insights.

La cuenta a nombre del cliente no es formalismo: si la relación termina, el histórico y el aprendizaje del pixel se quedan con quien pagó. Ya hay clientes cerrados en la cartera; esto se decide al principio o no se decide.

### 5. Lo que recibe el cliente

`00-AGC-Partners/05-Comercial-Adquisicion/DCE-Programa/08-Manual-Onboarding.md` es el manual oficial del programa: lo que se instala, el viaje de 90 días, las reglas del juego y el checklist del día 1. Personalízalo con los datos del cliente y entrégalo — no improvises un correo de bienvenida.

Antes de prometer alcance, contrasta con `05-Arquitectura-BOS.md` (los 7 componentes y las 3 fases) y con las exclusiones de `09-Contrato.md`. Prometer de más en el onboarding es donde se pierde un cliente en el mes 3.

### 6. Delegación

Terminada la carpeta, reparte y no ejecutes tú:

- `direccion-marketing` — perfil de cliente ideal, ángulos, plan de campaña. **Propuesta, no ejecución.**
- `direccion-ventas` — subcuenta y pipeline en GHL, propuesta comercial firmada al expediente.
- `direccion-finanzas` — alta en facturación, ficha de rentabilidad, condición de pago.
- `direccion-operaciones` — cadencia de reporte y checklist de calidad.

Cada dirección lee la ficha y escribe su resultado en la bóveda. No se pasan mensajes entre sí.

## Lo que este comando no hace

No crea campañas, no mueve presupuesto y no toca cuentas de Meta. Rige la regla heredada de ADS MANAGER: **por defecto, solo recomendar.** Ejecutar requiere `ejecuta` / `aplica` / `confirma` / `procede` de Diego.

## Cierre

Al terminar, entrega en máximo 8 líneas: nombre canónico, ruta de la carpeta, modalidad, los vacíos bloqueantes abiertos y qué dirección quedó con qué. Si algo no se pudo completar, dilo — un onboarding a medias declarado es útil; uno a medias reportado como listo cuesta un cliente.
