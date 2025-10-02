---
categoría: programación
tipo: js
---
# Programación en Nodejs

## Instalar node

Debe tener instalado node js. Para saber si lo tiene instalado, en una carpeta, abra una ventana de power shell/cmd/bash

Nota; si puede abrir una ventana de comando así: (shift+clic derecho / clic en: abrir ps aquí) o una ventana de bash (clic derecho/open git bash here) o vaya a su carpeta en el explorador de archivos de windows y en su barra de ruta ponga (cmd) o seleccione su carpeta y en el menu archivos de su explorador de archivos y seleccione (abrir windows power shell).

en su ventana de comandos ponga el comando:

```js
node --version
//versiones (solo en laa consola bash)
fnm list
fnm use 20.18.0
```
Si no reconoce el comando, instale node desde: [Download Node](https://nodejs.org/en/download)


## Aplicaciones simples

Puede programar sin crear un proyecto, si es una aplicacion muy pequeña. Probemos esto antes de crear un proyecto, vamos a crear un archivo simple por ejemplo (index.js)

En su editor de código VSCode cree un nuevo archivo:

Archivo: index.js
```js
let x=4
let y=5
let r=x+y
console.log("hola mundo x+y =", r)
```

En su consola de Power Shell (puede abrir una consola de ps en su VSCode, presionando ctrl+ñ) ejecute el comando:
```sh
node index.js
```

## inicializar proyecto node con npm

Con node viene la aplicación **npm** (node package manager) manejador de paquetes de node (un paquete es una biblioteca de node), npm es la aplicacion que usaremos para crear proyectos y administrar paquetes.

```sh
#crear carpeta de proyecto con camandos del shell:
mkdir proyecto #crear caréta
cd proyecto #moverse a la carpeta
#Tambíen puede crear la carpeta e ir a ella con el explorador de windows

#creear el proyecto
npm init 
#esto crea el archivo package.json 
#instalar paquetes
npm install nombre-paquete
#esto instala el paquete y lo registra en package.json
#mostrar una ista de paquetes instalados
npm ls
npm ls --depth 0
# ver si los paquetes tienen actualizaciones
npm outdated
# actualizar paquete por ejemplo eslint
npm up eslint
#actualizar todos los paquetes
npm up
#desinstalar modulo x ejemplo axios
npm un axios
#revisar riesgos de segurida en modulos del proyecto
npm audit 
#Puede ver la ruta de la vulnerabilidad y, a veces, npm le ofrece formas de corregirla:
npm audit fix
# fix no siempre puede resolver las  vunerabilidades
#puede forzar con el siguiente comando, sin embargo, antes de usarlo asegurese de que no afecta la ejecución de su proyecto
npm audit fix --force
```

Simplificando podemos inicializar un rpoyecto así:

```sh
# inicar proyecto
npm init
# o iniciar proyecto con los valores de default
npm init -y
```

## archivo package.json

cuando un proyecto se crea, se crea con el un archivo llamado **package.json**, donde se lleva un registro de los paquetes instlados, en ese archivo hay un conjunto de entradas en formato json que describen el proyecto con datos como nombre, autor, etcetera, una cosa mas, es que disponemos de una o mas entradas de **scripts** que son comandos de mi proyecto, su packge.json, se vera como el siguiente:
```json
{
  "name": "varios",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```
En este ejemplo aun no hay paquetes instalados, lo que ahora nos interesa son los scripts, vea que en el ejemplo en los scripts hay una entrada, "test", borre esa entrada y cambiela por las siguientes: 

```json
"devenv": "node --env-file=.env index.js"
"dev":"node index.js"
```
"dev" es un script que ejecuta con node el archivo index.js y desde el shell se ejecuta así:

```sh
npm run dev
```
La entrada "devenv" la usaremos mas adelante

## variables de entorno

crear un archivo .env y ponerlo en el gitignore, tambien poner el en gitignore node_modules  por cierto, el archivo .env tendra pares clave=valor

Ejempo de archivo .env:
Archivo: .env
```js
PORT=3000
DB_PLATFORM="sqlite"
SQLITE3_DB_NAME="dataBase.sqlite"
SQLITE3_DB_MEMORY=":memory:"
MYSQL_HOST=""
MYSQL_DB_NAME=""
MYSQL_USER=""
MYSQL_PASSWORD=""
URL="http://localhost"
```
Para gestionarlo
instalar la dependencia:
`npm i dotenv`

ahora para cargar en la variable global process.env los datos de env, lo hacemos asi:
```js
import dotenv from 'dotenv'
dotenv.config() //cargar los datos globalmente en processs.env
const PORT=process.env.PORT //obtenemos el puerto

```

## variables de entorno a partir de la version 20

A partir de la version 20, de manera nativa puede cargar varios archivos (o uno) con variables de entorno, ejemplo suponga que tiene el archivo .env, para cargarlo en node despues de la version 20 puede usar:

```sh
node --env-file .env index.js
# para cargar mas de un archivo con variables de entorno:
node --env-file=.env --env-file=config_db.env index.js
```

Esto cargará las variables de entorno de ambos archivos y las fusionará en el objeto process.env y ahora puede acceder a las variables de entorno:

```js
console.log(process.env.PORT)
console.log(process.env.DB_PLATFORM)
```

## watch

Es como un nodemon nativo:

```js
node --watch index.js
```

## vriables de entorno a partir de la version 22.10

[ver:](https://nodejs.org/en/blog/release/v22.10.0)

Las variables de .env se cargan directamente sin necesidad de una biblioteca

archivo .env
```
PORT=3000
```

Archivo: index.js
```js
process.LoadEnvFile()
console.log(process.env.PORT)
```
Ya esta estable:
```sh
node --watch index.js
```

## manejo de rutas de directorio path

process.cwd() "current work directory" es un método de Node.js que devuelve el directorio de trabajo actual del proceso de Node.js. Proporciona la ruta absoluta del directorio desde el que se inició el proceso de Node.js. Este directorio se suele denominar “directorio de trabajo actual” o “CWD”

```js
process.cwd() //devuelve el directorio de trabajo corriente del proceso de Node.js
```


