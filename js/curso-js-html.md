# js html
La integración de JavaScript en HTML es esencial para agregar interactividad y funcionalidad dinámica a sitios web. Existen varias formas de integrar JavaScript en HTML, pero la más común es a través de la etiqueta <script> en el código HTML.

Una forma de integrar JavaScript directamente en HTML es colocando el código JavaScript dentro de la etiqueta <script> en el código HTML. Por ejemplo:

```html
<script>
// tu código JavaScript aquí
</script>
```

O poniendo su código js en un archivo independiente
```html
<script src="miarchivo.js"></script>
```

**Nota** Se recomienda colocar el código JavaScript justo antes de cerrar la etiqueta </body>, ya que esto permite que todo el contenido HTML se cargue antes de ejecutar el código JavaScript.

## Evento onload

El evento onload en JavaScript se ejecuta cuando una página web (incluyendo todos sus recursos como imágenes, scripts y CSS) ha terminado de cargarse completamente. Se asocia comúnmente al objeto window o a elementos como <body>, y es útil para inicializar componentes que dependen de que todo el contenido esté listo.

```js
window.onload = function() {
    // Your initialization code here
};
```

Diferencia entre onload y DOMContentLoaded
Evento	            Descripción
window.onload	    Espera a que toda la página (imágenes, CSS, scripts) se cargue.
DOMContentLoaded	Se dispara cuando solo el DOM HTML está listo (sin esperar recursos externos). Más rápido.

```js
document.addEventListener("DOMContentLoaded", () => {
  console.log("DOM listo, pero imágenes/scripts pueden seguir cargando");
});
```

## Cargar datos asíncronos después del render:

```js
window.addEventListener("load", async () => {
  const response = await fetch("datos.json");
  const datos = await response.json();
  console.log(datos);
});
```

## eventos

```js
  document.querySelector("html").onclick = function () {
    alert("¡Ouch! ¡Deja de pincharme!");
  };
```

```html
<button type="button" onclick="document.write(5 + 6)">Try it</button>
```

## acceso a tags

```js
document.getElementById("demo").style.display = "none";
document.getElementById("demo").innerHTML = "My First JavaScript";
document.getElementById("demo").innerText = "Hello World";
document.getElementById('nuevo').classList.add('mi-clase');
document.getElementById('nuevo').classList.remove('mi-clase');
//
var el = document.querySelector(".miClase");
var el2 = document.querySelector("#foo");
//
document.write(5 + 6);
window.alert(5 + 6);
//
var div1Paras = div1.getElementsByTagName("p");
var num = div1Paras.length;
alert("Hay " + num + " <p> elementos en el elemento div1");
```

Los Selectores pueden ser muy útiles ejemplo. Aquí, será retornado el primer elemento <input name="login" /> dentro de <div class="user-panel main">.

```js
var el = document.querySelector("div.user-panel.main input[name='login']");
```


## formularios

acceso a formulario

```html
<form id="miFormulario">
  <input type="text" name="usuario">
  <button type="submit">Enviar</button>
</form>
```

```js
const formulario = document.getElementById('miFormulario');

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

acceder a los datos del formulario por:
```js
// Por ID (recomendado)
const formulario = document.forms.miFormulario; // o document.forms['miFormulario']

// Por índice (si es el primer formulario de la página)
const primerFormulario = document.forms[0];

//o usando:
const formulario = document.querySelector('#miFormulario');
```

Acceder a los campos de un formulatio

```js
const formulario = document.getElementById('miFormulario');

// Por nombre (recomendado)
const inputUsuario = formulario.elements.usuario; // o formulario.elements['usuario']

// Por índice
const primerCampo = formulario.elements[0];

// Valor del input
console.log(inputUsuario.value); // Muestra lo que el usuario escribió
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
  if (!formData.has('suscribir')) {
    datosJSON.suscribir = false; // Si el checkbox no está marcado
  }

  console.log(datosJSON);
  // Ejemplo de salida:
  // { nombre: "Juan", email: "juan@example.com", pais: "mx", mensaje
```

## ligas

[probar código](https://playcode.io/javascript)
[editor/compilador de código en línea](https://codesandbox.io/s/react-hook-form-get-started-j5wxo)
[jsplayground](https://www.jsplayground.dev/)
[probar css en linea](https://codi.link/%7C%7C)
[validar json](https://jsonlint.com/)
[Excalidraw](https://excalidraw.com/)
[caja de herramientas](https://omatsuri.app/)