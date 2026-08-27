# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Resumen

Página personal de Paco Novo. Todo el proyecto es **un único archivo autocontenido**: `index.html`, con el HTML, el CSS (`<style>` en el `<head>`) y el JavaScript (`<script>` al final del `<body>`) en el mismo fichero. No hay dependencias externas, ni gestor de paquetes, ni proceso de build, ni tests. El repositorio se versiona con git en la rama `main` y se publica en GitHub Pages.

## Comandos

No hay build, lint ni suite de tests. Para verlo en el navegador:

```bash
open index.html                 # abrir directamente desde el sistema de archivos
python3 -m http.server 8000     # o servirlo en http://localhost:8000
```

Todo cambio se verifica recargando la página en el navegador.

Para publicar (documentar, commitear en `main`, hacer push y desplegar en GitHub Pages) está el
comando `/dcpd`, definido en `.claude/commands/dcpd.md`.

Para revisar los textos en español de la página (ortografía, tono cercano y anglicismos) está la
skill `/text-reviewer`, definida en `.claude/skills/text-reviewer/SKILL.md`.

## Arquitectura

`index.html` tiene tres capas, y editar una suele exigir tocar las otras:

- **Tokens de color en `:root`**, redefinidos dentro de `@media (prefers-color-scheme: dark)` para el modo oscuro. Es el único mecanismo de tema del proyecto.
- **Secciones dentro de `<main>`**: `header` (nombre, rol y botón de Instagram), `#sobre-mi`, `#tareas` y `footer`. Las tarjetas (`header`, `section`) comparten un mismo patrón visual.
- **Lista de tareas**: la única parte con lógica. Estado en memoria (`tareas`, array de `{ id, text, done }`, y `filtroActual`), persistido en `localStorage` bajo la clave `'tareas'`. `render()` reconstruye por completo el `<ul>` desde cero: no hay actualización parcial del DOM, así que toda funcionalidad nueva de tareas debe pasar por ese repintado en lugar de manipular nodos existentes.

## Reglas del proyecto

@.claude/rules/estructura-y-dependencias.md
@.claude/rules/estilos-y-tema.md
@.claude/rules/estado-y-tareas.md
@.claude/rules/seguridad-y-dom.md
@.claude/rules/idioma-y-nombres.md
@.claude/rules/accesibilidad.md
