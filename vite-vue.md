## vue usando vue cli
[vue](https://vuejs.org/guide/quick-start)

Si aun no ha instalado vue/cli, instalelo asi:
```sh
npm i -q @vue/cli
```
Crear proyecto y Cargar biblioteca w3-css/bootstrap
```sh
#crear proyecto
#nota: el siguiente comando no funciona en la cosnola bash, debe usarlo en power shell
#en bash debe usar: winpty vue.cmd create nombreProyecto
npm create vue@latest
#en las opciones, poner nombre del proyecto, 
#en Add vue router for spa development poner (y), (n) en todo lo demas
#instalar w3-css
npm i w3-css
#o si lo prefiere, intalar bootstrap
npm i bootstrap
```
## configurar main.js para usar w3-css
En main.js:
```js
import 'w3-css/3/w3.css'
```
## modificar app.vue para w3-css
```html
<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>
<template>
  <div class="w3-row">
    <div class="w3-col l4">
        <nav clss="w3-bar w3-ligth-grey">
          <RouterLink class="w3-bar-item w3-button" to="/">Inicio</RouterLink>
          <RouterLink class="w3-bar-item w3-button" to="/about">Acerca de</RouterLink>
        </nav>
    </div>
    <div class="w3-col l4">
        <RouterView claass="w3-container"/>
    </div>
  </div>
</template>
<style scoped>

</style>
```

```sh
#ejecucion
npm run dev
```

### SweetAlert:
Un envoltorio práctico para sweetalert2

[alertas](https://vuejsexamples.com/a-convenient-wrapper-for-sweetalert2/)
[ejemplos en](https://sweetalert2.github.io)

instalar sweet alert
```sh
npm install -S vue-sweetalert2
```
Para usarlo; modificar el main.js así:
```js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import 'w3-css/3/w3.css'

import VueSweetalert2 from 'vue-sweetalert2'; //--sweetalet 
import 'sweetalert2/dist/sweetalert2.min.css'; //--sweetalet

const app = createApp(App)
app.use(VueSweetalert2); //--sweetalet
app.use(router)
app.mount('#app')
```

llamarlo así en el código:
```js
this.$swal('Hello world!');
#o
this.$swal.fire({
  title: "Good job!",
  text: "You clicked the button!",
  icon: "success"
  });
#o
this.$swal.fire({
  icon: "error",
  title: "Oops...",
  text: "Algo va mal!",
  footer: '<a href="#">Pore que tengo este rpobelam?</a>'
  });
#o

```
# vue con bootstrap

## configurar para bootstrap
En bootstrap en main.js requerimos el bootstrap
```js
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.bundle.js'
```

Datos del ejemplo para crear una api coid gecko:
ejemplo de coin gecko [datos](https://www.coingecko.com/es)
[tiene una api:](https://www.coingecko.com/api/documentation)
usaremos esta [liga http](https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false&locale=en)


# vue cli
Instalar vue cli
Por defecto esta deshabilitada la ejecucon de scripts en power shell, se puede verificar poniendo:
```sh
Get-ExecutionPolicy
#si devuleve Restricted, poner:
Set-ExecutionPolicy Unrestricted
#ahora  ya puedes ejecutar  vue-cli
vue -- version
#vue/cli 5.0.8
#crear proyecto
vue create proyecto
#agregar rutas
vue add router
```

# Ejemplo de serrvidor node
[ejemplo node cors](https://bluuweb.github.io/mevn/01-primeros-pasos/#instalar-cors-middleware)
