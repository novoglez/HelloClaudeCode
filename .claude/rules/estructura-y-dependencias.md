# Estructura y dependencias

- El proyecto es **un solo archivo autocontenido**, `index.html`. No añadas archivos `.css` o `.js` separados, ni un `package.json`, ni un paso de build, salvo que el usuario lo pida explícitamente.
- **Sin dependencias externas**: nada de CDNs, fuentes remotas, frameworks ni librerías de iconos. Los iconos se escriben como SVG inline (ver el de Instagram en el `header`). La tipografía es la pila del sistema ya definida en `body`.
- Orden dentro del archivo: `<style>` en el `<head>`, marcado en `<body>`, `<script>` al final del `<body>`. El JS asume que el DOM ya existe, así que no lo muevas al `<head>` sin `defer`.
- Indentación de 2 espacios. El contenido del bloque `<style>` sigue el sangrado ya presente en el archivo.
