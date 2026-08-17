---
name: trampas-entorno
description: Tres fallas del entorno de Diego que rompen scripts y disparan descargas de gigabytes
metadata:
  type: reference
---

**OneDrive con archivos en la nube.** Buena parte del Escritorio son marcadores, no archivos locales. Leerlos fuerza la descarga — `AGENTE ADS MANAGER` son 11,2 GB de video. Antes de recorrer en masa: filtrar por atributo o excluir media.

**PowerShell 5.1 lee `.ps1` como ANSI.** Un script escrito en UTF-8 con `ñ` o acentos falla al parsear. Escribir scripts solo en ASCII y resolver rutas con comodín: `'AGENTE PARA DISE*OS IA'`.

**Rutas con espacios y acentos.** Siempre `-LiteralPath` y comillas. Para comparar `git ls-files` contra el disco, usar `-c core.quotepath=false` — si no, escapa las rutas no-ASCII y todo parece distinto.

**Por qué importa:** las tres fallan en silencio o con un error que no apunta a la causa.

**Cómo aplicarlo:** son precondición de cualquier script o barrido de carpetas. Ver [[mapa-ecosistema]].
