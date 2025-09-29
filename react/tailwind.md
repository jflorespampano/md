## Vue con tailwind

[referencia original](https://tailwindcss.com/docs/guides/vite#vue)

##  con npm crearias el proyecto así: 
```sh
npm create vite@latest my-project -- --template vue
cd my-project
#instalar tailwind
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```js
#configurar templates en: tailwind.config.css
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
#agregar directivas a su style.css
@tailwind base;
@tailwind components;
@tailwind utilities;
```sh
#correr
npm run dev
#
```
ejemplo
```html
<template>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</template>
```

** nota a revisar ** : en el main.js agregar la linea: import './style.css'

```js
import {  creteApp } from 'vue'
import App from './App.vue'
import './style.css'
```

## otro ejemplo tailwind
[tomado de:](https://www.corecode.school/blog/tailwind-css-basico)

Antes que todo, asegúrate de tener Node.js instalado en tu equipo, esto para poder ejecutar comandos de npm.

Debes crear un nuevo proyecto de Vite.js:
```sh
npm create vite@latest my-tailwind-project -- --template vanilla
```
Después de crear el proyecto, navega hasta la carpeta y ejecuta el siguiente comando para instalar Tailwind:
```sh
npm install -D tailwindcss postcss autoprefixer
```
Para configurar Tailwind necesitas generar un archivo de configuración predeterminada, lo haces ejecutando el siguiente comando:
```sh
npx tailwindcss init -p
```
Se generará un archivo llamado tailwind.config.js en la raíz del proyecto. Este archivo permitirá agregar clases personalizadas a Tailwind de manera sencilla.
Además de tailwind.config.js, se generará automáticamente un archivo nombrado postcss.config.js que necesitas para utilizar las clases de Tailwind.

Este archivo contendrá el siguiente contenido:
```js
export default {
    plugins: {
        tailwindcss: {},
        autoprefixer: {},
    },
};
```
### tailwind, Configurando tus rutas de plantilla
Para que Tailwind pueda aplicar estilos a tus archivos, debes especificar las rutas en el archivo tailwind.config.js. Para hacerlo, agrega las rutas correspondientes en el parámetro content de la siguiente manera:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
      content: [
    "./index.html",
    "./src/**/*.{html,js,vue}"],
    theme: {
        extend: {},
    },
    plugins: [],
};
```
En este ejemplo, hemos incluido todas las rutas de los archivos con extensión .html. Asegúrate de ajustar las rutas a tu propia estructura de carpetas y archivos.

### agregando las directivas de taiwind a tu css
Vas al archivo style.css (CSS principal), aquí vas incluir directivas de procesador de CSS que se utilizan para incluir las utilidades predefinidas de Tailwind en tu hoja de estilo:
```js
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Estilos predefinidas por el proyecto de Vite.js */
```
Este archivo debe enlazarse en tu archivo HTML principal. En el archivo index.html importas style.css dentro de la etiqueta "head" de esta manera:

```html
<head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="./style.css" />
    <title>Vite App</title>
</head>
```
En este proyecto, hay algunos archivos predefinidos que vienen con la plantilla de Vite.js que no son necesarios, vas a hacer una limpieza.

En el archivo style.css, eliminarás todas las clases predefinidas para poder crear tus propias clases personalizadas. 

Para empezar, el archivo debería contener solo las siguientes líneas:
```js
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Aquí podrás agregar tus estilos personalizados */
```
Además, eliminarás completamente el archivo main.js y el enlace de "script" en tu index.html, ya que puede interferir con la estructura básica del proyecto:
```html
<body>
    <!-- ...Demás etiquetas -->
    <!-- Línea que debe ser elimindada -->
    <script type="module" src="/main.js"></script>
</body>
```
Por último borrarás javascript.svg, vite.svg y counter.js, que corresponden a archivos no utilizados.

Ahora que has configurado e integrado todo correctamente, puedes empezar a usar las clases de Tailwind en tu HTML.

Por ejemplo, puedes crear una sección con un título y dos párrafos utilizando las clases de Tailwind de la siguiente manera:
```html
<body>
    <section class="bg-gray-200">
        <h1 class="text-3xl font-bold text-center">Bienvenido a mi sitio web</h1>
        <p class="my-4">Este es un tutorial básico de Tailwind con Vite.js.</p>
        <p class="my-4">
            Tailwind es una biblioteca de clases CSS utilitarias diseñada para acelerar el proceso de diseño y desarrollo de sitios web.
        </p>
    </section>
</body>
```