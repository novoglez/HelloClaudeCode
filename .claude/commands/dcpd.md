---
description: Documenta, commitea en main, hace push a GitHub y despliega en GitHub Pages
argument-hint: "[mensaje de commit opcional]"
allowed-tools: Bash(git:*), Bash(gh:*), Bash(open:*), Bash(curl:*), Read, Edit, Write, Glob, Grep
---

# dcpd — Documentar, Commitear, Pushear, Desplegar

Ejecuta el ciclo completo de publicación de esta página. Mensaje de commit sugerido por el usuario: `$1` (si viene vacío, redáctalo tú a partir del diff).

Trabaja siempre en la rama `main`. No abras ramas nuevas ni pull requests.

## 1. Situar el repositorio

- Si no hay repositorio git (`git rev-parse --git-dir` falla), inicialízalo:
  - `git init -b main`
  - Crea un `.gitignore` mínimo con `.DS_Store`.
- Si el repo existe pero la rama actual no es `main`, cámbiate a `main` (`git switch main`, o `git branch -M main` si la rama principal aún tiene otro nombre) y trae los cambios pendientes contigo.
- Si no hay `origin`, créalo con `gh repo create HelloClaudeCode --public --source=. --remote=origin` (repo del usuario, `novoglez`). Confirma con el usuario antes de crear un repositorio público nuevo.

## 2. Actualizar la documentación

Antes de commitear, revisa qué ha cambiado (`git diff`, `git status`, y el estado actual de `index.html`) y actualiza la documentación para que siga siendo cierta:

- **`CLAUDE.md`**: el resumen, la lista de secciones de `<main>` y la descripción del estado de la lista de tareas deben coincidir con `index.html`. Si el proyecto ya tiene git y despliegue, la frase «ni control de versiones» debe dejar de estar ahí, y los comandos deben incluir cómo se publica.
- **`.claude/rules/*.md`**: si un cambio ha introducido un token de color nuevo, una sección nueva, un campo nuevo en los objetos de tarea o un patrón de DOM nuevo, refléjalo en la regla correspondiente.

No inventes documentación de cosas que no existen: documenta solo lo que está en el archivo. Si nada ha cambiado funcionalmente, no toques la documentación.

Todo el texto de la documentación va **en español**, como el resto del proyecto.

## 3. Commit en `main`

- `git add -A`
- Commit con un mensaje en español, en imperativo y en una línea (por ejemplo `Añade filtro de tareas completadas`). Usa `$1` si el usuario lo ha proporcionado.
- Cierra el mensaje con el pie de coautoría habitual de Claude Code.
- Si no hay nada que commitear, dilo y sigue al paso 4 (puede quedar pendiente un push o un despliegue).

## 4. Push a GitHub

- `git push -u origin main` la primera vez, `git push origin main` después.
- Si el push es rechazado por divergencia, **no** fuerces: haz `git pull --rebase origin main`, resuelve y vuelve a intentarlo. Si hay conflicto que no sea trivial, para y pregunta.

## 5. Desplegar

El sitio es un único `index.html` estático, así que el despliegue es **GitHub Pages sirviendo la raíz de `main`**:

- Comprueba si Pages ya está activo: `gh api repos/{owner}/{repo}/pages`.
- Si devuelve 404, actívalo: `gh api repos/{owner}/{repo}/pages -X POST -f "source[branch]=main" -f "source[path]=/"`.
- Si ya estaba activo, fuerza una reconstrucción: `gh api repos/{owner}/{repo}/pages/builds -X POST`.
- Espera a que el último build quede en `status: built` (`gh api repos/{owner}/{repo}/pages/builds/latest`), reintentando unas pocas veces. Si se queda en `errored`, informa del error y no digas que está desplegado.

## 6. Informar

Termina con un resumen breve:

- Qué documentación se ha actualizado.
- El hash y el mensaje del commit.
- Que el push a `origin/main` está hecho.
- La URL pública del sitio y el estado del último build.

Si algún paso se ha saltado (nada que commitear, Pages ya al día), dilo explícitamente en lugar de darlo por hecho.
