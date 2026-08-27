# Estado y lista de tareas

- El estado vive en dos variables de módulo: `tareas` (array de `{ id, text, done }`) y `filtroActual`. No introduzcas fuentes de verdad paralelas ni guardes estado en el DOM.
- **Ciclo obligatorio para cualquier cambio**: mutar `tareas` → `guardarTareas()` → `render()`. No actualices nodos del DOM a mano: `render()` reconstruye el `<ul>` entero desde cero y cualquier retoque manual se pierde en el siguiente repintado.
- La persistencia es `localStorage` con la clave `'tareas'`. `cargarTareas()` ya envuelve el `JSON.parse` en `try/catch` y valida con `Array.isArray`; mantén esa tolerancia a datos corruptos si cambias el formato guardado.
- Si cambias la forma de los objetos guardados, ten en cuenta que hay datos previos en el navegador del usuario: la carga debe seguir funcionando con el formato antiguo o normalizarlo.
- El filtrado es solo de presentación (`tareasFiltradas()`); nunca filtres mutando `tareas`.
- El mensaje de lista vacía sale de `textoVacio()`, que mira `tareas.length` y `filtroActual` para no decir «Aún no hay tareas» cuando lo que está vacío es solo el filtro. Si añades un filtro nuevo, añádele también su texto ahí.
- `id` se genera con `Date.now()`. Si añades creación en lote, garantiza unicidad antes de confiar en él.
