# Accesibilidad

- Todo control sin texto visible necesita `aria-label` en español (ver el botón `×` de eliminar y el enlace de Instagram).
- Los SVG decorativos llevan `aria-hidden="true"`; el nombre accesible lo aporta el texto del enlace o su `aria-label`.
- Los botones dentro de `<form>` que no envían llevan `type="button"` explícito (los filtros ya lo hacen), para no disparar el submit.
- Los enlaces externos usan `target="_blank"` junto con `rel="noopener noreferrer"`.
- Mantén un estilo de foco visible en los controles interactivos. `#tarea-input` anula el `outline` pero lo compensa con `border-color: var(--accent)` en `:focus`; si copias ese patrón, incluye siempre la señal de foco alternativa.
