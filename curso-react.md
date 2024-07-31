# React

React es una biblioteca JavaScript de código abierto, basada en componentes, para construir interfaces de usuario rápidas y dinámicas.

Para usar React debe tener instalado node js. Para saber si lo tiene instalado, en una carpeta, abre una ventana de power shell(ps) usa las teclas: (shift+clic derecho / clic en abrir ps aquí).

Escribe el comando:

```sh
node --version
```
Si no reconoce el comando, instale **node** desde: [Download Node](https://nodejs.org/en/download)

Con node se descarga la aplicación **npm** (node package manager) manejador de paquetes de node (un paquete es una biblioteca de node), esta aplicacion la que usaremos para crear proyectos en React.

## Vite

Vite (palabra francesa para "rápido", pronunciada /vit/, como "veet") es una herramienta de construcción que tiene como objetivo proporcionar una experiencia de desarrollo más rápida y eficiente para proyectos web modernos, permitiendo crear la estructura de tu proyecto de manera facil y rápida. Consta de dos partes principales:

- Un servidor de desarrollo que proporciona numerosas mejoras de funciones con respecto a los módulos ES nativos, por ejemplo, reemplazo de módulo en caliente (HMR) extremadamente rápido.

- Un comando de compilación que agrupa su código con Rollup, preconfigurado para generar activos estáticos altamente optimizados para producción.


## crear proyecto react con vite

Con Vite puede crear proyectos para varias plantillas de desarrollo (Vanilla, Vue, React, Svelte). Puede especificar directamente el nombre del proyecto y la plantilla que desea utilizar mediante opciones de línea de comando adicionales. Por ejemplo, para crear la plantilla de un proyecto Vite + React, ejecute:

Crear proyecto con vite+react, en la consola:
```sh
# abrir la consola de Power Shell
# shift+clic derecho/seleccionar - abrir ventana de power shell aquí
# escriba el siguiente comando para crear un proyecto React con vite, dando el nombre del proyecto
npm create vite@latest nombreProyecto -- --template react
# Crearlo en vanilla js seria: npm create vite@latest nombre -- --template vanilla
# para crear el proyecto seleccionando las diferetes opciones de plantilla, usa el comando
npm create vite@latest nombreProyecto
# o el siguiente comando; y solicitará también el nombre del proyecto
npm create vite@latest
# o usando la version instalada/ si no la encuentra busca la última
npm create vite
# una vez creado ir a la carpeta del nuevo proyecto
cd nombre
# instalar dependencias
npm install # se puede abreviar como: npm i
# ejecutar aplicación
npm run dev
```

Lo anterior lo podemos resumir en 4 comandos:

```sh
npm create vite 
# contestar las preguntas
# una vez creado ir a la carpeta del nuevo proyecto
cd nombre
npm install
npm run dev
```
npm run dev, arranca un servidor, en tu navegador y te muestra una liga para ir a el. Abre la liga que te muestra en la ventana de Power Shell y veras tu aplicación en ejecución.

Ve a la ventana de PS y deten el servidor presionando ctrl+c

## Adaptando la plantilla a nuestro proyecto

Ve a la sub-carpeta src de tu proyecto, borra todos los archivos excepto main.jsx, sustituye el contenido del archivo main.jsx por lo siguiente:

Archivo: main.jsx
```js
import React from 'react'
import ReactDom from 'react-dom/client'

const root=ReactDom.createRoot(document.getElementById('root'))
root.render(<h1>hello world</h1>)
```

Prueba tu aplicación ejecutando el comando (npm run dev)

## Crear un componente

Ahora crearemos un nuevo componente llamado Greeting:

Archivo: main.jsx
```js
import React from 'react'
import ReactDom from 'react-dom/client'

function Greeting() {
  return (
    <h1> Greeting </h1>
  )
}

const root=ReactDom.createRoot(document.getElementById('root'))
root.render({Greeting()})
```

React usa jsx, en jsx el componente, se puede llamar así:

```js
root.render(
    <div>
        <Greeting />
    </div>
)
```

## Crear el componente en otro archivo:

Lo mas recomendable es crear cada componente en su propio archivo para aumentar la reusabilidad.

En la carpeta **src** crear el archivo Greeting.jsx (debe iniciar en mayuscula):

Archivo:Greeting.jsx
```js
export function Greeting() {
    return (
      <h1> Greeting desde un archivo </h1>
    )
  }
```
y el archivo main.jsx queda:

```js
import ReactDOM from 'react-dom/client'
import { Greeting } from './Greeting'
const root=ReactDom.createRoot(document.getElementById('root'))

root.render(
    <div>
        <Greeting />
    </div>
)
```

Nota: Si en VScode tiene instalda la extensión: ES7+Reac/Redux, puede crear el componente mediante un sniipet, escriba: rafc <tab>

Nota: Antes en los componentes, debia importar: 
```js
import React from 'react'
``` 
al inicio del archivo de su componete, sin embargo en las versiones mas recientes esto no es necesario, pero deberá importar React si usa Hooks u otos elementos de React.

## cargar css para un componente

Si desea usar estilos desde un archivo css, en su componente por ejemplo en Saludo.jsx, ponga:

```js
import "./Saludo.css"
export const Saludo = () => {
  return (
    <div className="title">
        <h2>Titulo</h2>
        <div className="container">
            <pre>
                contenido de ...
            </pre>
        </div>
    </div>
  )
}

```

El archivo Saludo.css
```css
.container {
    padding: 40px;
    text-align: left;
    background: #f7df1e;
    color: #3c3a2d;
  }

  .title {
    padding: 40px;
    text-align: center;
    background: #173f8f;
    color: #fff;
  }
```

## Props

Los props son los parámetros que se envian a los componentes.
Enviar props a componentes
en el llamado:

```jsx
<Saludo titulo="titulo uno" contenido="Contenido uno" />
```

En el componente:
```js
import "./Saludo.css"
// eslint-disable-next-line react/prop-types
export const Saludo = ({titulo="sin titulo",contenido="contenido"}) => {
  return (
    <div className="title">
        <h2>{titulo}</h2>
        <div className="container">
            <pre>
                {contenido}
            </pre>
        </div>
    </div>
  )
}
```

## Cargar prop types:

Biblioteca para manejo de tipos de datos en React

Instalar prop-types
```sh
npm install --save prop-types
```

Para usar prop types:

En el llamado se envian los props normalmente:

```js
import ReactDOM from 'react-dom/client'
import { Saludo } from './Saludo'
const root=ReactDOM.createRoot(document.getElementById('root'))

root.render(
  <div>
    <Saludo titulo="titulo uno" />
  </div>
)

```

Al recibir los props, para añadirles tipos:
```js
import PropTypes from 'prop-types'

export const Saludo = ({titulo}) => {
  return (
    <h2>{titulo}</h2>
  )
}

Saludo.propTypes={
  titulo: PropTypes.string.isRequired
}
```
Aqui estamos diciendo que el tipo del prop es string y es obligatorio enviar el prop

# Estados

En un componente para que React haga seguimiento de una variable y actualice sus dependencias cuando la variable cambie, se requiere usar estados:

```js
import { useState } from "react";

export const Saludo = () => {
  const [dato,setDato]=useState("Ningun mensaje")

  const onClick=()=>{
    setDato("Nuevo mensaje")
  }

  return (
    <div>
      <h2>{dato}</h2>
      <button onClick={onClick}>click aqui</button>
    </div>
  )
}
```

dato es la variable y setDato es la funcion a la que hay que llamar para actualizar la variable dato.

# cargar datos desde un fetch

Crear la funccion para leer datos:

Archivo fetchData.js
```js
export const fetchData = async () => {
  try {
    const response= await fetch('https://jsonplaceholder.typicode.com/users')
    const data= await response.json()
    return {
        data,
        isLoading: false
    }
  } catch (error) {
    console.log(error)
  }
}
```

Creamos un Hook para manejar el estado de los datos:
Archivo: useFetchData.js
```js
import { useEffect, useState } from "react";
import { fetchData } from "../helpers/fetchData";

export const useFetchData = () => {
  const [data, setData] = useState([])
  const [isLoading, setIsLoading] = useState(true)
  const getData = async ()=>{
    const {data, isLoading} = await fetchData()
    setData(data)
    setIsLoading(isLoading)
  }
  useEffect(()=>{
    getData()
  },[])

  return {
    data,
    isLoading
  }
}
```

Usamos los datos recuperados en un componente:

Archivo: UserList.jsx
```js
import { useFetchData } from "../libs/useFetchData"
// eslint-disable-next-line react/prop-types
export const UserList = () => {
    const {data, isLoading} = useFetchData() 
  return (
    <>
        <ul>
            {isLoading? 
            <p>cargando...</p>
            :data.map(item=><li key={item.id}>{item.name}</li>)}
        </ul>
    </>
  )
}
```

Archivo: main.jsx
```js
import React from 'react'
import ReactDOM from 'react-dom/client'
import { Principal } from './components/Principal.jsx'
import { UserList } from './components/UserList.jsx'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <UserList />
  </React.StrictMode>,
)

```

## Ejemplo estructura de carpetas para el ejemplo del fetch

Necestaremos una aplicación react y crear las carpetas:
|
+ src +
      + components +
                   + UserList.jsx
      + helpers +
                + fetchData.js
      + hooks +
              + useFetchData.js
      + main.jsx

Archivo msin.jsx
```js
import ReactDOM from 'react-dom/client'
import { UserList } from './components/UserList'
const root=ReactDOM.createRoot(document.getElementById('root'))
root.render(
  <div>
    <UserList />
  </div>
)

```

Archivo UserList.jsx
```js
import { useFetchData } from "../hooks/useFetchData"
export const UserList = () => {
    const {data, isLoading} = useFetchData()
    console.log("🚀 ~ file: UserList.jsx:4 ~ UserList ~ data:", data)
  return (
    <>
        <ul>
            {isLoading? 
            <p>cargando...</p>
            :data.map(item=><li key={item.id}>{item.name}</li>)}
        </ul>
    </>
  )
}

```

Aechivo: useFetchData.js
```js
import { useEffect, useState } from "react";
import { fetchData } from "../helpers/fetchData";

export const useFetchData = () => {
  const [data, setData] = useState([])
  const [isLoading, setIsLoading] = useState(true)
  const getData = async ()=>{
    const {data, isLoading} = await fetchData()
    setData(data)
    setIsLoading(isLoading)
  }
  useEffect(()=>{
    getData()
  },[])

  return {
    data,
    isLoading
  }
}

```

Archivo: fetchData.js
```js

export const fetchData = async () => {
  try {
    const response= await fetch('https://jsonplaceholder.typicode.com/users')
    const data= await response.json()
    return {
        data,
        isLoading: false
    }
  } catch (error) {
    console.log(error)
  }
}

```

# Enrutamiento <a name="router"></a>

## Cargar el paquete react-router-dom
```sh
npm i react-router-dom
```

### cargar el objeto BrouserRouter

El objeto BrouserRouter debe envolver la aplicación React; 
 
Archivo: main.jsx
```js
import React from 'react'
import ReactDOM from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </BrowserRouter>
  ,
)

```

### Importar w3css en el index.html para poner estilos

Para poner estilos usaremos **w3css**

Archivo: index.html
```js
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
    <title>Rutas react</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

## Crear el componente NavBar.jsx

Archivo: NavBar.jsx
```js
import { NavLink } from "react-router-dom"

export const NavBar = () => {
  return (
    <div className="w3-bar w3-border w3-light-grey">
        <NavLink to='/' className="w3-bar-item w3-button">Home</NavLink>
        <NavLink to='/mostrar' className="w3-bar-item w3-button">Mostrar</NavLink>
        <NavLink to='/altas' className="w3-bar-item w3-button">Altas</NavLink>
        <NavLink to='/buscar' className="w3-bar-item w3-button">Buscar</NavLink>
    </div>
  )
}
```

## Crear los destinos de las rutas, por ejemplo:

Archivo Mostrar.jsx
```js
export const Mostrar = () => {
  return (
    <div>Mostrar</div>
  )
}
```

## Usar las rutas:
Archivo App.jsx
```js
import { Route, Routes, Navigate } from 'react-router-dom'
import { NavBar } from './NavBar'
import { Home } from './Home'
import { Mostrar } from './Mostrar'
import { Altas } from './Altas'
import { Buscar } from './Buscar'
import './App.css'

function App() {

  return (
    <>
      <div className='w3-container'>
        <NavBar />
        <Routes>
          <Route path="/" element={<Home/>}></Route>
          <Route path="/mostrar" element={<Mostrar/>}></Route>
          <Route path="/altas" element={<Altas/>}></Route>
          <Route path="/buscar" element={<Buscar/>}></Route>
          <Route path="/*" element={<Navigate to='/' />}></Route>
        </Routes>
      </div>
    </>
  )
}

export default App

```


# Miscelanea

## eslint
es el linter de js, agregarlo a complementos de code

## notas
* En vite los componentes empiezan con mayusculas

## comandos
Comando: rafce en vscode para crear componente rapido debemos tener instalado
en ES7+

## Hooks

para manejar estados en react
por ejemplo useState, useEfect
si ven un codigo en react que empiese con use es un hook

- react developer tool extension para navegador
para depurar react

- para ejercicio 5 gifs
inscribirse y obtener apikey
request: https://api.giphy.com
api key : LSQA1CBorhzJ4SgFcqimkf4BwdSpYuoX


# Crear proyecto react con create-app

[documentacion](https://create-react-app.dev/docs/getting-started)

Para crearlo con create-react-app:
```sh
#crear proyecto react con create app
npx create-react-app my-app
cd my-app
npm start
```

Si lo creaste con creat-react-app, ve a la carpeta src y borra todos los archivos, crea el archivo index.js vacio y agrega el siguiente código:

index.js
```js
import React from 'react'
import ReactDom from 'react-dom/client'

const root=ReactDom.createRoot(document.getElementById('root'))
root.render(<h1>hello world</h1>)
```
Listo, tu primera aplicacion React


Nota: opcionalmente si desea que las lineas largas se muestren en la misma pantalla usando varias lineas, agregue a su settings.json que tiene la configuracion de su editor, la linea:
```js
"editor.wordWrap": "on"
```

## Agregar componente en React
Agregar un componente, para agregar un componente, (por ahora en el mismo archivo index.js), agregue al archivo index.js el código de la función Greeting:

Archivo:index.js
```js
import React from 'react'
import ReactDom from 'react-dom/client'

const root=ReactDom.createRoot(document.getElementById('root'))

function Greeting() {
    return (
      <h1> Hola mundo crudelio </h1>
    )
  }

root.render(
    <div>
        { Greeting()}
    </div>
)
```
En React el root.render se puede es ecribir así:

```js
    <div>
        <Greeting />
    </div>
```

Crear el componente en otro archivo:
En la carpeta src crear el archivo Greeting.js (debe iniciar en mayuscula):

Archivo:Greeting.js
```js
export function Greeting() {
    return (
      <h1> Hola mundo crudelio </h1>
    )
  }
```

y el archivo index.js queda:
```js
import ReactDOM from 'react-dom/client'
import { Greeting } from './Greeting'
const root=ReactDom.createRoot(document.getElementById('root'))

root.render(
    <div>
        <Greeting />
    </div>
)
```

##  usar React Query

instalar el query
```sh
npm i react-query
```

opcionalmente como herramienta de depuracion de query agregar en main.jsx:
import { ReactQueryDevtools } from 'react-query/devtools'

en el archivo: main.jsx
```js
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'
import { QueryClientProvider, QueryClient } from 'react-query'
import { ReactQueryDevtools } from 'react-query/devtools'

const queryClient=new QueryClient()

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <App />
      <ReactQueryDevtools/>
    </QueryClientProvider>
  </React.StrictMode>,
)

```

## React material ui

[instalar](https://mui.com/material-ui/getting-started/installation/)

Material UI es una biblioteca de componentes de interfaz de usuario para React, diseñada para ayudar a los desarrolladores a construir aplicaciones web modernas, siguiendo los principios de Material Design, el sistema de diseño creado por Google. Proporciona una amplia variedad de componentes predefinidos, como botones, formularios, iconos, cuadros de diálogo, tablas, etc. Es posible utilizarla con Styled Components.

[Ejemplo de material table](https://github.com/mbrn/material-table)

## React datatable

```bash
npm install react-data-table-component
# o si no tiene instalado styled components
npm install react-data-table-component styled-components
```
[React data table](https://react-data-table-component.netlify.app/?path=/docs/getting-started-installation--docs)
[ejemplo](https://www.freecodecamp.org/news/create-tables-using-the-react-datatable-component-library/)

## styledd components

[styled components](https://www.escuelafrontend.com/styled-components-en-react)


## ligas

[Ref: Fazt code](https://www.youtube.com/watch?v=rLoWMU4L_qE&t=0s)

[blog Guerra](https://www.cesarguerra.mx/configuracion-rapida-de-eslint-con-standard-js-para-proyectos-de-javascript-y-de-react-con-vite-js/)

[github Guerra](https://github.com/warderer/taller-react-unacar-2023)

[tools herramienta cambia de html a jsx](https://transform.tools/html-to-jsx)

[Inicio rápido de React en español](https://es.react.dev/learn)

[Ejemplo de formulario](https://github.com/fazt/react-hook-form-tutorial/blob/master/src/App.jsx)

[use context](https://es.react.dev/reference/react/useContext)

[enrutamiento](#router)