---
name: cartera-reconciliada
description: La cartera real de AGC al 16-ago-2026 tras cruzar 20 cuentas de Meta contra tres listados que no coincidían
metadata:
  type: project
---

Al 16-ago-2026 la cartera quedó en **4 clientes que pagan** (Óptica Ferreira, Sweet Mayorista, MQFJOYAS, Kristus) y **2 sin cobro** (Pelucas Antonella Avatte — madre de Diego; MASAIFIT Calama — hermana de Kristus). Todo lo demás está cerrado.

**Por qué importa:** convivían tres versiones del listado —7 en el Registro Maestro, 11 en `AGENTE ADS MANAGER/CLAUDE.md`, 20 cuentas reales en Meta— y ninguna coincidía. Dos `account_id` en uso activo no existían en Meta: las consultas fallaban sin error visible y las cifras se atribuían mal.

**Cómo aplicarlo:** el detalle vive en `AGENTE DE PROCESO/00-AGC-Partners/00-Registro-Maestro-Clientes.md`, que es la única fuente. Ningún `account_id` se usa de memoria ni de un documento antiguo — se verifica contra `ads_get_ad_accounts` primero. Los cerrados con `valor_documental: alto` (Importadora Carlitos, Distribuidora Odawe) no se archivan: alimentan los manuales de método. Ver [[riesgo-concentracion]].
