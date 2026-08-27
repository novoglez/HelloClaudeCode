# Construcción del DOM

- El contenido que escribe el usuario se inserta con `textContent` y nodos creados con `document.createElement`. **No uses `innerHTML` para pintar tareas** ni construyas HTML concatenando strings con datos del usuario.
- `lista.innerHTML = ''` para vaciar el contenedor es aceptable y es el único uso permitido: no interpola nada.
- Los listeners se registran sobre el nodo recién creado dentro de `render()`. Como el `<ul>` se reconstruye entero, no hace falta desregistrarlos.
