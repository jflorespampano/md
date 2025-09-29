# Curso react Guerra Gurrero sep 2023

## lint/linter

Nos permite detectar código sospechoso, confuso o incompatible
EsLINT es el linter de JS. Instale el complemento ESLINT en vscode

## Complementos en VSCode

* ES7+ React/Redux, React-Native snippets
* ESLint

## crear proyecto react

En la consola ejecutar:
```sh
npm create vite@latest nombre -- -- template react
#una vez creado ir a la carpeta
cd nombre
npm insatall
npm run dev
```

## Configurar eslint

Normalmente para usar ESLint necesitaríamos ejecutar el comando npm init @eslint/config y comenzar a establecer la configuración inicial para indicarle a ESLint como debe interpretar y corregir nuestro código, sin embargo es posible ahorrarnos esta parte y usar una configuración estandarizada y muy popular para proyectos en JavaScript, la cuál se llama Standard JS.

Primero, necesitamos instalar Standard JS como dependencia de desarrollo en nuestro proyecto:

```sh
npm i standard -D`
```

Una vez instalado Standard JS, bastará con añadir su configuración de ESLint en el archivo package.json de nuestro proyecto, por lo que debemos agregar estas lineas al final del archivo pero justo antes de cerrar la última llave `}`

```json
  "eslintConfig": {
    "extends": [
      "./node_modules/standard/eslintrc.json"
    ]
  }
```

El día 20 de Abril de 2023, Vite actualizo su herramienta para crear un nuevo proyecto (create vite), donde ahora incluye un nuevo archivo .eslintrc.cjs para realizar la configuración del Linter, incluso ya viene con una configuración de fábrica, pero sí aún así queremos usar las reglas de Standard JS, solo debemos hacer lo siguiente:

En el archivo .eslintrc.cjs, en el apartado de extends, añadir las reglas ‘standard’ y ‘standard-jsx’, quedando de la siguiente forma dicho apartado:

```json
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:react/jsx-runtime',
    'plugin:react-hooks/recommended'
    'standard',
    'standard-jsx'
  ],
```

## notas
* En vite los componentes empiezan con mayusculas

## snippets

snippet: rafce en vscode para crear componente rapido debemos tener instalado
el complemento ES7+ React/Redux, React-Native snippets

```jsx
import React from 'react'

const ToDoList = () => {
  return (
    <div>ToDoList</div>
  )
}

export default ToDoList
```

## Hooks

para manejar estados en react
por ejemplo useState, useEfect
si ven un codigo en react que inicie con la palabra use es un hook

## extensiones para el navegador

react developer tool extension para navegador
para depurar react

## ligas

[blog Guerra](https://www.cesarguerra.mx/configuracion-rapida-de-eslint-con-standard-js-para-proyectos-de-javascript-y-de-react-con-vite-js/)

[github Guerra](https://github.com/warderer/taller-react-unacar-2023)

[tools herramienta cambia de html a jsx muy buena](https://transform.tools/html-to-jsx)


