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
En la página (no recomendada) : https://json-generator.com/ 
[Otra:](https://www.jsongenerator.io/)
[Otra:](https://mockaroo.com/)
tenemos un generdor de datos json , esto es muy util para hacer pruebas

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
# instalar json-server
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

Puede arrancar el servidor así:
```sh
npx json-server db.json
```
O peuede agrear al package.json, en la  lista de scripts, la entrada:

```json
"back": "json-server --watch db/products.json --port 3000"
```
En la nueva version se pude omitir --watch
```json
"back": "json-server db/products.json --port 3000"
```

puede arrancar el servidor json así:
```sh
npm run back
```

Listo en el puerto 3000 se tiene un servidor que devuelve datos json.
se consulta así:
```
http://localhost:3000/products
http://localhost:3000/products/1
```

### json-server con npx

```sh
# ejecutar json-server con npx
npx json-server data.json -p 3000
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
npm install
npm run start
```
con run start: node ./bin/www
o: node --env-file=.env ./bin/www

[Con express](https://www.npmjs.com/package/express)

[Crear proyecto express](https://www.npmjs.com/package/express-create-app)

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