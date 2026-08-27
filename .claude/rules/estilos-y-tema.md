# Estilos y tema

- **Ningún color literal en una regla CSS.** Todo color sale de un token de `:root` (`--bg`, `--bg-card`, `--text`, `--text-muted`, `--accent`, `--accent-contrast`, `--border`, `--danger`). Si necesitas un color nuevo, añade el token en `:root` y su equivalente en el bloque `@media (prefers-color-scheme: dark)`; nunca solo en uno de los dos.
- La única excepción actual es `rgba(229, 72, 77, 0.12)` (fondo del hover de eliminar). Si tocas esa regla, conviértela en token en lugar de replicar el patrón.
- El modo oscuro se resuelve **redefiniendo tokens**, no duplicando selectores. No escribas reglas nuevas dentro del `@media` que no sean redefiniciones de variables.
- Las tarjetas (`header`, `section`) comparten el mismo patrón: `background: var(--bg-card)`, `border: 1px solid var(--border)`, `border-radius: var(--radius)`, `box-shadow: var(--shadow)`, `padding: 1.75rem`. Una sección nueva se ve como las demás o no encaja.
- Medidas en `rem`; radios de pastilla con `999px`. Las transiciones son cortas (`0.15s`–`0.2s ease`) y solo sobre color, borde u opacidad.
