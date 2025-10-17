---
categoría: programación
tipo: js
---

# js html

La integración de JavaScript en HTML es esencial para agregar interactividad y funcionalidad dinámica a sitios web. Existen varias formas de integrar JavaScript en HTML, pero la más común es a través de la etiqueta <script></script> en el código HTML.

Una forma de integrar JavaScript directamente en HTML es colocando el código JavaScript dentro de la etiqueta <script></script> en el código HTML. Por ejemplo:

```html
<script>
// tu código JavaScript aquí
</script>
```

O poniendo su código js en un archivo independiente
```html
<script src="miarchivo.js"></script>
```

## Donde cargar el script

En un documento HTML, los scripts de JavaScript se pueden cargar en dos lugares principales: dentro del `<head>` o justo antes del cierre del `</body>`. La ubicación afecta el rendimiento y la funcionalidad.

1. **En el `<head>`**:
    
    - Tradicionalmente, los scripts se colocaban en el `<head>`. Sin embargo, cuando el navegador encuentra un script en el `<head>`, detiene la renderización de la página hasta que el script se descarga y ejecuta. Esto puede causar que la página se muestre más lentamente al usuario (bloqueo de renderizado).
    - Para mitigar esto, a menudo se usa el atributo `defer` o `async` cuando se coloca en el `<head>`.
        
2. **Justo antes del cierre del `</body>`**:
    
    - Colocar los scripts al final del body asegura que el HTML se cargue y renderice primero, lo que mejora la percepción de velocidad. Los scripts no bloquearán la renderización de la página.
        

Atributos importantes para scripts:

- `defer`: Indica que el script se ejecutará una vez que el documento HTML haya sido completamente analizado, pero antes del evento `DOMContentLoaded`. Los scripts con `defer` mantienen el orden de ejecución según su aparición en el documento.
    
- `async`: El script se ejecutará de manera asíncrona, es decir, tan pronto como esté disponible, sin esperar a que el analizador del HTML continúe. El orden de ejecución no está garantizado.
    

Recomendaciones:

- Si el script no depende del DOM y no es crítico, se puede usar `async` (en el `<head>` o en el `<body>`).
- Si el script depende del DOM o de otros scripts, y necesita ejecutarse en orden, es mejor usar `defer` en el `<head>` o colocarlo al final del `<body>` sin `defer` (aunque `defer` en el `<head>` es generalmente mejor para la carga porque no bloquea el analizador).

Ejemplos:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Mi página</title>
  <script src="mi-script.js" defer></script>
</head>
<body>
  <!-- Contenido de la página -->
</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<head>
  <title>Mi página</title>
</head>
<body>
  <!-- Contenido de la página -->

  <script src="mi-script.js"></script>
</body>
</html>
```

## Evento onload

El evento **onload** en JavaScript se ejecuta cuando una página web (incluyendo todos sus recursos como imágenes, scripts y CSS) ha terminado de cargarse completamente. Se asocia comúnmente al objeto **window** o a elementos como `<body>`, y es útil para inicializar componentes que dependen de que todo el contenido esté listo.

```js
window.onload = function() {
  // su código de inicialización aquí
  document.write(5 + 6);
};
```

```js
document.addEventListener("DOMContentLoaded", () => {
  console.log("DOM listo, pero imágenes/scripts pueden seguir cargando");
});
```

Diferencia entre onload y DOMContentLoaded

| Evento           | Descripción                                                                                |
| ---------------- | ------------------------------------------------------------------------------------------ |
| window.onload    | Espera a que toda la página (imágenes, CSS, scripts) se cargue.                            |
| DOMContentLoaded | Se dispara cuando solo el DOM HTML está listo (sin esperar recursos externos). Más rápido. |


## Cargar datos asíncronos después del render:

```js
window.addEventListener("load", async () => {
  const response = await fetch("datos.json");
  const datos = await response.json();
  console.log(datos);
});
```

## Eventos

Asignar eventos:
```html
<button onclick="document.write(5 + 6)">haz clic</button>
<input type="button" onclick="alert('Hello World!')" value="pruebame">
<inout type="button" id="miBoton" value="pincha aqui">
<input type="submit" value="Enviar">
<input type="submit">
```

Eventos dinámicos:
```js
  document.querySelector("miBoton").onclick = function () {
    alert("¡Ouch! ¡Deja de pincharme!");
  };
```


## Acceso a tags


```html
<div class="w3-text-red" id="demo">
	<p id="mensaje">texto rojo</p>
</div>
<inout type="button" id="miBoton" value="pincha aqui">
```

```js
document.querySelector("miBoton").onclick = function () {
    document.getElementById("demo").style.display = "none";
	document.getElementById("demo").innerHTML = "<p>My First JavaScript</p>";
	document.getElementById("mensaje").innerText = "Hello World";
	document.getElementById('demo').classList.add('w3-gray');
	document.getElementById('demo').classList.remove('w3-gray');
};

//referenciar todos los elementos de una clase, devuelve un arreglo
var array_el = document.querySelector(".miClase");
//referencias un elemento con id="foo"
var el = document.querySelector("#foo");
//
document.write(5 + 6);
window.alert(5 + 6);
//acceder a todos los parrafos, devuelve un arreglo
var div1Paras = div1.getElementsByTagName("p");
var num = div1Paras.length;
alert("Hay " + num + " <p> elementos en el elemento div1");
```

Los Selectores pueden ser muy útiles, ejemplo: Aquí, será retornado el input:
```html
<div class="user-panel main"> 
	<input name="login" />
</div>
```

```js
var el = document.querySelector("div.user-panel.main input[name='login']");
```


## Objetos en js

![[curso-node-objetos]]
## map

![[curso-node-arreglos#map]]

## funciones

![[curso-node-funciones]]
## formularios

Ejemplos de querySelctor
```js
const header = document.querySelector('#header');
const botones = document.querySelectorAll('.boton');
const formulario = document.querySelector('form#principal');
const formulario = document.getElementById('principal');
```

acceso a formulario

```html
<form id="miFormulario">
  <input type="text" name="usuario">
  <button type="submit">Enviar</button>
  <input type="submit">
</form>
```

```js
const formulario = document.getElementById('miFormulario');
const formulario = document.querySelector('#miFormulario');

// Ejemplo: Escuchar evento de envío
formulario.addEventListener('submit', (e) => {
  e.preventDefault(); // Evita que se recargue la página
  //enviar formulario
  const formulario = document.getElementById('miFormulario');
  const formData = new FormData(formulario);
  const datosJSON = Object.fromEntries(formData.entries());
  console.log(datosJSON);
  console.log(JSON.stringify(datosJSON);)
  console.log('Formulario enviado');
});
```

### acceder al formulario con forms
```js
// Por ID (recomendado)
const formulario = document.forms.miFormulario; // o document.forms['miFormulario']
// Por índice (si es el primer formulario de la página)
const primerFormulario = document.forms[0];
//o usando:
const formulario = document.querySelector('#miFormulario');
```


### Acceder a los campos de un formulario

```js
const formulario = document.getElementById('miFormulario');
// Por nombre (recomendado)
const inputUsuario = formulario.elements.usuario; // o formulario.elements['usuario']
// Por índice
const primerCampo = formulario.elements[0];
// Valor del input
console.log(inputUsuario.value); // Muestra lo que el usuario escribió

```

### querySelector

```html
<form id="miFormulario">
    <input type="text" name="usuario" placeholder="Nombre de usuario">
    <input type="password" name="contrasena" placeholder="Contraseña">
</form>
```
```js
// Acceder al input de usuario dentro de todo el documento
const inputUsuario = document.querySelector('input[name="usuario"]');
console.log(inputUsuario.value); // Muestra el valor del input

// Acceder al input de contraseña dentro de un formulario específico
const form = document.querySelector('#miFormulario');
const inputContrasena = form.querySelector('[name="contrasena"]');
console.log(inputContrasena.value);
```
### getElementsByName
```html
<form id="miFormulario">
    <input type="text" name="usuario" value="john_doe">
    <input type="email" name="email" value="john@example.com">
    <input type="radio" name="genero" value="masculino" checked>
    <input type="radio" name="genero" value="femenino">
</form>
```
```js
// Acceder al input de usuario
const inputsUsuario = document.getElementsByName('usuario');
const inputUsuario = inputsUsuario[0]; // Primer elemento
console.log(inputUsuario.value); // "john_doe"

// Acceder a los radio buttons
const radiosGenero = document.getElementsByName('genero');
console.log(radiosGenero.length); // 2 (ambos radio buttons)

// Encontrar el radio button seleccionado
let generoSeleccionado;
for (let radio of radiosGenero) {
    if (radio.checked) {
        generoSeleccionado = radio.value;
        break;
    }
}
console.log(generoSeleccionado); // "masculino"
```

### acceder x medio del id

```html
<input type="text" id="usuario" placeholder="Nombre de usuario">
<input type="email" id="correo" value="ejemplo@mail.com">
```

```js
// Usando el selector de ID (#)
const inputUsuario = document.querySelector('#usuario');
const inputCorreo = document.querySelector('#correo');
```
### Acceder por variables globales window (no es una buena práctica)

un comportamiento histórico en los navegadores: cuando se asigna un `id` a un elemento HTML, ese `id` se convierte en una propiedad global (variable) en el objeto `window`. Sin embargo, esto no es una buena práctica y puede llevar a conflictos.

```js
// Los elementos con ID se convierten en variables globales
console.log(usuario.value);    // Funciona si existe id="usuario"
console.log(correo.value);     // Funciona si existe id="correo"
```
## obtener todos los campos de un formulario en un json

```js
const formulario = document.getElementById('miFormulario');

formulario.addEventListener('submit', (e) => {
  e.preventDefault();
  
  // Paso 1: Crear un objeto FormData
  const formData = new FormData(formulario);
  // Paso 2: Convertir FormData a un objeto plano
  const datosJSON = Object.fromEntries(formData.entries());
  // Paso 3 (Opcional): Manejar checkboxes/radios no seleccionados
  // formData.has() se usa para verificar si un objeto FormData contiene una clave (field) específica. Retorna true si la clave existe, false si no.
  if (!formData.has('suscribir')) {
    datosJSON.suscribir = false; // Si el checkbox no está marcado
  }
  console.log(datosJSON);
  // Ejemplo de salida:
  // { nombre: "Juan", email: "juan@example.com", pais: "mx", mensaje
```

## ligas

[IDE js en linea jsplayground](https://www.jsplayground.dev/)
[IDE como jsplayground pero mas avanzada](https://playcode.io/javascript)
[IDE avanzado de código en línea](https://codesandbox.io/s/react-hook-form-get-started-j5wxo)
[probar css en linea](https://codi.link/%7C%7C)
[validar json](https://jsonlint.com/)
[Excalidraw](https://excalidraw.com/)
[caja de herramientas](https://omatsuri.app/)
[generador de datos aleatorio](https://www.mockaroo.com/)
[fakerjs para node](https://fakerjs.dev/guide/)