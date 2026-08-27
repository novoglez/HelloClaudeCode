# Idioma y nomenclatura

- Todo en **español**: texto visible, comentarios, `aria-label`, `placeholder` y también los identificadores del código (`tareas`, `filtroActual`, `agregarTarea`, `eliminarTarea`, `#lista-tareas`, `.filtro-btn`, `.activo`). No mezcles inglés en nombres nuevos.
- La única excepción son las propiedades de los objetos ya persistidos (`id`, `text`, `done`): están en `localStorage` de los usuarios y renombrarlas rompe los datos existentes.
- `id` y `class` en `kebab-case`; variables y funciones en `camelCase`; constantes de módulo en `SCREAMING_SNAKE_CASE` (`STORAGE_KEY`).
- El documento es `<html lang="es">`. Manténlo.
