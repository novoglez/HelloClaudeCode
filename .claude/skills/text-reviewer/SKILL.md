---
name: text-reviewer
description: Revisa los textos visibles del proyecto (español) buscando faltas de ortografía y tildes, tono distante o acartonado y anglicismos evitables. Úsala cuando el usuario pida revisar, corregir o mejorar los textos, copys, mensajes o etiquetas de la página, y también antes de publicar cambios que añadan o modifiquen texto visible.
---

# text-reviewer — Revisión de textos

Revisa el texto que lee una persona en la página y propone correcciones. No toca lógica, estilos ni estructura: solo cadenas de texto.

## Qué se revisa

Todo el texto en español que llega al usuario final, esté donde esté:

- Contenido visible de `index.html`: `<title>`, encabezados, párrafos, botones, enlaces, `<footer>`.
- Texto de interfaz que no se ve pero se lee: `placeholder`, `aria-label`, `alt`, `title`.
- Cadenas generadas desde JavaScript (contador, mensajes de lista vacía, textos creados con `textContent`).
- Documentación del repositorio (`CLAUDE.md`, `.claude/rules/*.md`, `.claude/commands/*.md`) cuando el usuario lo pida explícitamente.

No se revisan: nombres de variables, funciones, `id`, `class` ni claves de `localStorage`. Esos siguen las reglas de `.claude/rules/idioma-y-nombres.md` y cambiarlos rompe código o datos guardados.

## Criterios

### 1. Ortografía y gramática

- Tildes, incluidas las de diacrítico (`mí`/`mi`, `sé`/`se`, `más`/`mas`, `té`/`te`) y las mayúsculas acentuadas (`Añadir`, `Éxito`).
- Signos de apertura obligatorios: `¿…?` y `¡…!`.
- Concordancia de género y número, y singular/plural correcto en textos con contador (`1 tarea pendiente` frente a `2 tareas pendientes`).
- Puntuación: espacio después de coma y punto, nunca antes; puntos suspensivos como `…` o `...`, pero de forma coherente en todo el archivo.
- Comillas tipográficas `«»` o `“”` de forma coherente; nada de comillas rectas mezcladas.

### 2. Tono cercano

El registro de la página es personal y directo: primera persona, frases cortas, sin solemnidad.

- Tutea o habla en primera persona (`Mis tareas`, `Sobre mí`). Nada de `usted` ni de impersonales fríos (`Se deberá introducir…`).
- Verbos en activa y en imperativo amable en los controles (`Añadir`, `Eliminar tarea`), no sustantivos abstractos (`Realización del alta`).
- Frases de una idea. Si una frase pasa de unas 25 palabras o tiene dos subordinadas encadenadas, pártela.
- Sin jerga corporativa (`gestionar`, `optimizar`, `solución integral`) ni exclamaciones de más. Cercano no es efusivo.
- Los mensajes de estado vacío o de error acompañan, no regañan (`Aún no hay tareas` en vez de `No se han encontrado registros`).

### 3. Sin anglicismos

Sustituye el anglicismo cuando exista un equivalente natural en español:

| Evita | Usa |
| --- | --- |
| task, to-do | tarea |
| item | elemento, tarea |
| link | enlace |
| click, clicar | pulsar, hacer clic |
| loading | cargando |
| check / checkear | marcar, comprobar |
| deletear, borrar (de delete) | eliminar |
| feature | función, funcionalidad |
| setting | ajuste, opción |
| default | por defecto, predeterminado |
| tip | consejo |
| email | correo |
| skills | habilidades, conocimientos |
| about me | sobre mí |

Se aceptan sin traducir los nombres propios y las marcas (`Instagram`, `GitHub`, `GitHub Pages`, `JavaScript`, `localStorage`) y los términos técnicos que solo aparecen en documentación para desarrolladores. La regla de idioma es para el texto que lee el visitante.

## Cómo trabajar

1. Localiza el texto: `grep -nE '<h[12]|<p|<title|<button|placeholder=|aria-label=|alt=' index.html` y las cadenas literales del `<script>`.
2. Anota cada problema con su línea, la categoría (ortografía / tono / anglicismo) y la corrección propuesta.
3. Presenta primero el informe: una lista de `index.html:línea` — texto actual → texto propuesto — motivo en una frase. Ordena por gravedad: primero las faltas, luego los anglicismos, luego el tono.
4. Aplica los cambios solo si el usuario lo pide o si ya te dio permiso para corregir. Al aplicarlos, edita únicamente la cadena de texto, sin reformatear el marcado que la rodea.
5. Si un texto es correcto pero mejorable, dilo como sugerencia opcional y sepáralo de lo que es un error real.

No inventes hallazgos: si el texto está bien, dilo en una línea y termina.
