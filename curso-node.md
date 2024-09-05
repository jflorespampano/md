# Programación en Nodejs

## Instalar node

Debe tener instalado node js. Para saber si lo tiene instalado, en una carpeta, abra una ventana de power shell (shift+clic derecho / clic en: abrir ps aquí) o una ventana de bash.

ponga el comando:

```js
node --version
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


## modulos (desde youtube: desarrollo Util)

Los módulos son la forma en que organizamos nuestro proyecto en diferetes archivos, un nódulo es simplemente un archvo con extensión .js (tambien puede ser extensiones .mjs o .cjs).

Existen 2 formas de trabajar con modulos en node, un modulo es un archivo con código js que puede exportar elementos tales como funciones, clases y objetos.
Las dos formas son:

1. CommonJS que usa la sentencia **require**, archivos con extencion js (o cjs)
2. ESM (ecma script module) que usan la sentencia **import**, archivos con extencion mjs

**Nota CommonJS (es el que usa node por defecto)**

## Crear un modulo de CommonJS

Por ejemplo creamos el modulo: operaciones

Archivo:operaciones.js
```js
const suma=(n1,n2)=> return n1+n2
const resta=(n1,n2)=> return n1-n2
const multiplicacion=(n1,n2)=> return n1*n2
const division=(n1,n2)=> return n1/n2
console.log(module) //muestra lo que module contiene
module.exports={suma, resta, multiplicacion, division}
```

En el archivo **main.js**
```js
//importar el modulo
const operaciones = require('./operaciones')

console.log(operaciones.suma(2,3))
```

**Nota: Con require se puede importar json, el archivo json no debera tener module.exports**

## Usar commonjs 

Se puede definir en el proyecto el tipo de modulos a usar (commonjs o esm) de dos formas, en el archivo package.json (creado con el comando npm init):

* para definir que se usará Commonjs, en el archivo package.json, no poner nada o poner la entrada: 
**"type":"commonjs"**
* para usar modulos de tipo ESM poner la entrada: 
**"type":"module"**

## Usar modulos ESM

Para usar el sistema module ESM
Los archivos tendran la extension .mjs o pueden tener extencion .js y tener la entrada "type":"module" en el package.json.

### Exportar importa en ESM:

Archivo: operaaciones.mjs
```js
const suma=(n1,n2)=> {return n1+n2}
const resta=(n1,n2)=> {return n1-n2}
const multiplicacion=(n1,n2)=> {return n1*n2}
const division=(n1,n2)=> {return n1/n2}

export {suma, resta, multiplicacion, division}
export default suma
```
Otra forma de escribir el archivo operaciones.mjs
```js
export const data=[
    {name:"ana"},
    {name:"luis"},
    {name:"paco"},
    {name:"sergio"},
    {name:"rosa"}
]
export const suma=(n1,n2)=> {
    return n1+n2
}
export const resta=(n1,n2)=> {
    return n1-n2
}
export const multiplicacion=(n1,n2)=> {
    return n1*n2
}
export const division=(n1,n2)=> {
    return n1/n2
}
```

en el main.js
```js
//importar desestructurando
import {suma, resta, multiplicacion, division} from './operacines.mjs'
//o importar el default
import suma from './operacines.mjs'
```

|                    Uso                      |              sintaxis               |
|---------------------------------------------|-------------------------------------|
|importar un modulo completo                  | import * as name from ‘module-name’ |
|importar el export default de 1 modulo       | import name from ‘module-name’      |
|importar una exportacion unica               | import { name } from ‘module-name’  |
|importar multiples exportaciones             | import { nameOne , nameTwo } from ‘module-name’ |
|importar un modulo solo para efectos laerales| import ‘./module-name’              |


## Cambios según el tipo de modulos

En commonjs puede usar __dirname, __filename, tambien importar archivos json

En ESM no se puede importar archivos json, tampoco se puede usar el __dirname, ni el __filename.
Para hacerlo, hay que saber que el import es un objeto:

console.log(import.meta.url)

## usar commonjs desde ESM (Ecma Script Module)

**Nota en el archivo package.jon debe tener la entrada "type": "module"**

si tenemos un archivo .cjs lo importamos así:
```js
import {suma} from './operaciones.cjs'
```

Cargar un archivo .json
```js
import {createRequire} from 'module'
const require=createRequire(import.meta.url)

const user=require('./users.json')
console.log(user)

```

Usar __dirname, __filename en ESM
```js
import { dirname } from 'path';
import { fileURLToPath } from 'url';

const __dirname = dirname(fileURLToPath(import.meta.url));
const __filename = fileURLToPath(import.meta.url);

console.log("🚀 ~ file: index.js:9 ~ __filename:", __filename)
console.log("🚀 ~ file: index.js:10 ~ __dirname:", __dirname)
```

## usar ESM desde Commonjs

Podemos usar import dinamicos, por ejemplo
Archivo: prueba.mjs
```js
const data=[
    {id:1,nombre:"juan"},
    {id:2,nombre:"luis"},
    {id:3,nombre:"pablo"},
]
export default function suma(){
    return 34
}
export {suma,data}
```
Si tenemos un archivo .mjs, lo cargamos con una **importación dinámica**, así:
```js
import('./prueba.mjs')
.then((module)=>{
    console.log(module.suma(3,4))
    //console.log(module.default.suma(2,3))
})
```

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

## variables de entornno a partir de la version 20

A partir de la version 20, de manera nativa puede cargar varios archivos (o uno) con variables de entorno, ejemplo suponga que tiene el archivo .env, para cargarlo en node despues de la version 20 puede usar:

```sh
node --env-file .env index.js
# para cargar mas de un archivo con variables de entorno:
node --env-file .env --env-file .envdevelopment index.js
```
y ahora puede acceder a las variables de entorno:

```js
console.log(process.env.BACKEND_URL)
console.log(process.env.DB_USR)
```

## watch

Es como un nodemon nativo:

```js
node --watch index.js
```

## data fake
En la página: https://json-generator.com/ 
tenemos un generdor de datos json , esto es muy util para hacer pruebas

# usar express

Biblioteca para manejo de peticions http

## Cargar express en su proyecto
```sh
#iniciar proyecto con los valores de default
npm init -y
#cargar express
npm i express
#cargar dotenv
npm i dotenv
```

Crear archivo: .env
```js
PORT=3000
```
agregar la entrada: "type":"module", al package.json

## middleware

Ejemplo de recepcion de datos de diferetes formas en express
y usando el middleware json() y text() podemos recibir datos del body en post, put
con un body en formato texto  o json

```js
import express from "express"
import dotenv from 'dotenv'

dotenv.config() //cargar las variables de entorno del archivo .env en process.env
const PORT=process.env.PORT //cargar el numeo de puerto

const app=express()
//middleware para  aceptar json y texto
app.use(express.json())
app.use(express.text())
app.use(express.urlencoded({extended:false}));
app.get("/",(req,res)=>{
    res.set({"content-type":"text/html; charset=utf-8"})
    res.end(
        `
        <h1>Hola mundo</h1>
        `
    )
})
//parametros en la url
//espera una url asi: http://localhost:3000/user/779-jflores-59
app.get("/user/:id-:name-:edad",(req,res)=>{
    res.set({"content-type":"text/html; charset=utf-8"})
    //params almacena los  parametros enviados por la url
    console.log(req.params)
    res.end(
        `
        <h1>${req.params.name} binevenidos a express id=${req.params.id}</h1>
        `
    )
})
//parametros query
//espera:http://localhost:3000/search?id=779&nombre=alejandro flores&edad=59
app.get('/search',(req,res)=>{
    const data=req.query
    console.log(data)
    res.send(
        `
        <h1>${data.id} bienvenido ${data.nombre} tu edad ${data.edad}</h1>
        `
    )
})
//parametros en el body
//espera:http://localhost:3000/account, con un body en formato json o Form-encode
app.post('/account',(req,res)=>{
    console.log(req.body)
    res.send(
        `
        <h2>Hola recibiendo POST ${req.body.nombre} edad ${req.body.edad}</h2>
        `
        )
})
app.put('/account',(req,res)=>{
    console.log(req.body)
    res.send(
        `
        <h2>Hola recibiendo PUT ${req.body.nombre} edad ${req.body.edad}</h2>
        `
        )
})
app.patch('/account',(req,res)=>{
    console.log(req.body)
    res.send(
        `
        <h2>Hola recibiendo PATCH ${req.body.nombre} edad ${req.body.edad}</h2>
        `
        )
})

//espera id comom parametro query: http://localhost:3000/search?id=779
app.delete('/account',(req,res)=>{
    console.log(req.query)
    res.send(
        `
        <h2>Hola recibiendo con DELETE un id=${req.query.id}</h2>
        `
        )
})

app.listen(PORT,()=>{
    console.log(`iniciando express desde: http://localhost:${PORT}/`)
})
```

# Usar SQlite

## Crear una base de datos en SQLite

```js
const sqlite3 = require('sqlite3').verbose();
// const db = new sqlite3.Database(':memory:');
let datos = [
    {
        "userId": 1,
        "id": 1,
        "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
        "body": "quia et suscipit\nsuscipit recusandae consequuntur architecto"
    },
    {
        "userId": 1,
        "id": 2,
        "title": "qui est esse",
        "body": "est rerum tempore  molestiae ut reiciendis\nqui aperiam non debitis po nisi nulla"
    }
]


function crearTabla(db) {
    db.serialize(() => {
        const sql = `CREATE TABLE IF NOT EXISTS posts(
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            userId INTEGER NOT NULL,
            title TEXT NOT NULL,
            body  TEXT NOT NULL
        ); `
        db.run(sql);

        const stmt = db.prepare("INSERT INTO posts(userId, title, body) VALUES (?,?,?);");
        datos.forEach(e => {
            stmt.run(e.userId, e.title, e.body);
        });

        stmt.finalize();

        db.each("SELECT * FROM posts;", (err, row) => {
            console.log(row.id + ": " + row.title);
        });
    });

    //db.close();

}

db = new sqlite3.Database('posts.sqlite3', (err) => {
    if (err) {
        console.log('Could not connect to database', err)
    } else {
        console.log('Connected to database');
    }
});
crearTabla(db);
db.close();
```

## Getionar datos de una base de datos

```js
import sqlite3 from 'sqlite3'
import { open } from 'sqlite'

//para depuracion
sqlite3.verbose();

async function muestra() {
    // open the database
    const db = await open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    });
    const result = await db.all('SELECT * FROM posts');
    db.close();
    console.log(result);
}
async function leerUnDato() {
    const db = await open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    });
    const result = await db.get('SELECT * FROM posts WHERE id = ?', '1')
    console.log(result);
}
async function insertaDato({ id, userId, title, body }) {
    const db = await open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    });
    const sql = `INSERT INTO posts(userId,title,body) VALUES (${userId},'${title}','${body}')`;
    const result = await db.run(sql);
    console.log('resultado:', result);
    db.close();
    muestra();
}

async function actualizaDato({ id, userId, title, body }) {
    const db = await open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    });
    const sql = `update posts set userId=${userId}, title='${title}', body='${body}' where id=${id}`;
    const result2 = await db.run(sql)
    console.log(result2);
    db.close();
    muestra();
}
/////////////////////////////////////// promesas ///////////////////////////////
function muestraCnPromesa(callback) {
    open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    }).then((db) => {
        db.all('SELECT * FROM posts')
            .then((result) => {
                callback('salida', result);
                // console.log(result);
            })
            .then(() => {
                db.close().then(() => {
                    console.log('cerrada la bd');
                });
            });
    });
}

function insertaDatoCnPromesa({ id, userId, title, body }, callback) {
    open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    }).then(db => {
        const sql = `INSERT INTO posts(userId,title,body) VALUES (${userId},'${title}','${body}')`;
        db.run(sql)
            .then(result => {
                callback('****** salida: ', result);
                // console.log(result);
            })
            .then(() => {
                db.close().then(() => {
                    console.log('cerrada la bd');
                });
            }).catch(error => {
                console.log('error en la consulta', error);
            });
    }).catch((error) => {
        console.log('error al abrir la bd', error);
    });
}

function actualizaDatoCnPromesa({ id, userId, title, body }) {
    open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    }).then(db => {
        const sql = `update posts set userId=${userId}, title='${title}', body='${body}' where id=${id}`;
        db.run(sql)
            .then(result => {
                console.log(result);
            })
            .then(() => {
                db.close().then(() => {
                    console.log('cerrada la bd');
                });
            }).catch(error => {
                console.log('error en la consulta', error);
            });
    }).catch((error) => {
        console.log('error al abrir la bd', error);
    });
}

muestraCnPromesa(console.log);

```

## manejo de rutas de directorio path

```js
process.cwd() //devuelve el directorio de trabajo corriente del proceso de Node.js
```
### mostrar pdf
[Mostrar pdf](https://mozilla.github.io/pdf.js/examples/index.html#interactive-examples)

# expresione regulares

## resumen regex

. - matches any character except for newline characters
| - matches either of the expressions separated by it
^ - matches the beginning of the string
$ - matches the end of the string
* - matches the preceding expression zero or more times
+ - matches the preceding expression one or more times
? - matches the preceding expression zero or one times
[] - matches any single character in the brackets
() - groups expressions together

Las propiedades de acceso estáticas RegExp.$1,…, RegExp.$9 devuelven coincidencias de subcadenas entre paréntesis.

# Recursos

## instalar json-server SERVIDOR JSON LOCAL

[ref](https://www.npmjs.com/package/json-server)

```sh
npm i json-server
```
crear un archivo json, pej: en la carpeta db: db/products.jon con los datos
```js
{
    "products":[
        {
            "id":1,
            "name":"laptop",
            "description":"laptop gaming",
            "price":1000,
            "inStock":true
        }
        //...resto de los datos
    ]
}
```
Agrear al package.json, en la  lista de scripts, la entrada:

```json
"back": "json-server --watch db/products.json --port 3000"
```

arrancar el servidor json así:
```sh
npm run back
```

Listo en el puerto 3000 se tiene un servidor que devuelve datos json.
se consulta así:
```
http://localhost:3000/products
http://localhost:3000/products/1
```

## crear proyectos
usando modulos common js
[crear proyectos con express](https://expressjs.com/es/starter/generator.html)

## crar proyectos (ok)
Para crear un proyecto node con express puede tambien usar el generador de proyectos:
```sh
#instaar el genrador de proyectos
npm install -g express-generator@4
# crear el proyectco por ejemplo con el motor de vsitas ejs
express nodeServer --view=ejs
cd nodeSerever
npm innstall
npm run start
```
con run start: node ./bin/www
o: node --env-file=.env ./bin/www

[Con express](https://www.npmjs.com/package/express)

## extension para chrome

[Extension para visualizar mejor los json](https://chromewebstore.google.com/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh?pli=1)

##  poner en produccion

PM2 es un administrador de procesos (demonio) que lo ayudará a administrar y mantener su aplicación en línea. Comenzar a usar PM2 es sencillo, se ofrece como una CLI simple e intuitiva, instalable a través de NPM.



```sh
npm install pm2@latest -g
pm2 start server.js
pm2 delete server.js # cierra las aplicaciones
pm2 delete all # cierra las aplicaciones
pm2 list #muestra unalista con todos los proceso manejados por pm2
```
El app-name (server.js en el ejemplo) pude sustituirse por el id del proceso o por la  palabra all
Ecosistema
Archivo: ecosystem.config.js
```js
module.exports = {
  apps : [{
    name   : "mastereye",
    script : "./server.js",
    args   : "limit"
  }]
}
```

```sh
pm2 start ecosystem.config.js
```

## node-windows

Descripción: node-windows es una biblioteca de Node.js que proporciona soporte para servicios de Windows, registro de eventos, UAC y métodos auxiliares para interactuar con el sistema operativo. Permite instalar, iniciar, detener y desinstalar scripts de Node.js como servicios de fondo en entornos de producción.
```sh
npm i node-windows

```
## ligas
[path](https://nodejs-es.github.io/api/path.html)

[documentacion pm2](https://pm2.keymetrics.io/docs/usage/quick-start/)

[node-windows](https://www.npmjs.com/package/node-windows)

[react query](https://tanstack.com/query/v3)

[npm json-server](https://www.npmjs.com/package/json-server)

[Generador de dataFakes](https://www.mockaroo.com/)

[Data fakes](https://jsonplaceholder.typicode.com/)

[Mostrar documentos pdf](https://mozilla.github.io/pdf.js/examples/index.html#interactive-examples)

[Como firmar un xml (c#)](https://learn.microsoft.com/es-es/dotnet/standard/security/how-to-sign-xml-documents-with-digital-signatures)

[canonicalizar](https://josemmo.medium.com/xml-y-canonicalizaci%C3%B3n-7002c42442dd)

[regex](https://dev.to/emilossola/mastering-regular-expressions-in-nodejs-a-comprehensive-guide-4hl5)

[muy bueno](https://www.arkaitzgarro.com/javascript/capitulo-11.html)

[referencia sqlite3 español](https://www.digitalocean.com/community/tutorials/how-to-use-sqlite-with-node-js-on-ubuntu-22-04)

[get, each, all sqlite](https://discuss.codecademy.com/t/why-use-db-each-instead-db-all-or-db-get-in-node-sqlite/381382)