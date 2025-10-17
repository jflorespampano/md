---
categoría: herramientas
tipo: editor
---
# snippet (retazo)

Es un fragmento de código en una plantilla reutilizable que permite insertar bloques de código predefinidos.
VS Code incluye snippets predeterminados para muchos lenguajes (ej: for en JavaScript o div en HTML).


Se istalan snippets al instalar Extensiones como:

* ES7+ React/Redux Snippets (para React).
* Python Snippets (para Python).
* HTML Snippets.

## Cómo crear tu propio snippet

* Abre el menú de snippets:
* Ctrl + Shift + P (Windows/Linux) o Cmd + Shift + P (Mac).
* Escribe "Configure User Snippets" y selecciona el lenguaje (ej: JavaScript).

Define el snippet por ejemplo para un console.log() rápido:

```json
{
  "Quick Console Log": {
    "prefix": "clog",  // Palabra clave para activar
    "body": [
      "console.log('$1', $2);"  // $1 es un placeholder
    ],
    "description": "Inserta un console.log rápido"
  }
}
```
* prefix: Palabra que activa el snippet.
* body: Código que se insertará.
* $1, $2: Posiciones del cursor después de insertar.

Guarda y usa:

Escribe clog en un archivo JavaScript y presiona Tab.

## generador de snippet's

En la siguiente liga encontrarás un generados de snippets.

[generados snippets](https://snippet-generator.app/?description=&tabtrigger=&snippet=&mode=vscode)

Uso:
* generamos el snippet
* lo copiamos
* Para agregarlo a Vscode:
archivo/preferencias/configurar fragmentos de usuario
ahí, seleccionamos para que lenguajes estará disponible
una vez echo eso, añadirlo al json

para usarlo poner la palabra que lo dispara y presionar tab

## mis snipets

