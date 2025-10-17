
# Recursos

## data fake

En la página (no recomendada) : https://json-generator.com/ 
[jsongenerator:](https://www.jsongenerator.io/)
[mockaro:](https://mockaroo.com/)
tenemos un generdor de datos json , esto es muy util para hacer pruebas

### mostrar pdf
[Mostrar pdf](https://mozilla.github.io/pdf.js/examples/index.html#interactive-examples)


## instalar json-server SERVIDOR JSON LOCAL

[jsonserver](https://www.npmjs.com/package/json-server)

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

## paquete moment

biblioteca muy popular para manejar y manipular fechas y horas en Node.js.
Aunque moment es muy útil, últimamente muchas personas han estado migrando a alternativas más ligeras como date-fns o dayjs, ya que moment se considera una biblioteca bastante pesada

`npm install moment
`
```js
const moment = require('moment');

// Obtener la fecha y hora actual
const now = moment();
console.log(now.format('MMMM Do YYYY, h:mm:ss a')); // Ejemplo: October 14th 2024, 7:47 pm

// Sumar y restar tiempo
const futureDate = now.add(7, 'days');
const pastDate = now.subtract(7, 'days');
console.log(futureDate.format('MMMM Do YYYY'));
console.log(pastDate.format('MMMM Do YYYY'));

// Manipulación y formateo
const customDate = moment('2024-12-25');
console.log(customDate.format('dddd, MMMM Do YYYY')); // Ejemplo: Wednesday, December 25th 2024

```

## day.js Alternativa ligera a moment

`npm install dayjs`

```js
const dayjs = require('dayjs');

// Obtener la fecha y hora actual
const now = dayjs();
console.log(now.format('MMMM D, YYYY h:mm A')); // Ejemplo: October 14, 2024 7:48 PM

// Sumar y restar tiempo
const futureDate = now.add(7, 'day');
const pastDate = now.subtract(7, 'day');
console.log(futureDate.format('MMMM D, YYYY'));
console.log(pastDate.format('MMMM D, YYYY'));

// Manipulación y formateo
const customDate = dayjs('2024-12-25');
console.log(customDate.format('dddd, MMMM D, YYYY')); // Ejemplo: Wednesday, December 25, 2024

```

## herramientas

### playground

Probar código en js

[jsplayground](https://www.jsplayground.dev/)

### visualizar json en graficos interactivos

[jsoncrack](https://jsoncrack.com/)

### caja de herramientas

[omatsuri](https://omatsuri.app/)

### herramienta para hacer apps responsivas

[responsively](https://responsively.app/)

### validador de json

[validador json](https://jsonlint.com/)

## temas adicionales

[gridjs](https://gridjs.io/docs/config/pagination)
[generar datos falsos](https://www.npmjs.com/package/@faker-js/faker)


## fnm administraador de versiones de node

El comando fnm (Fast Node Manager) es un administrador de versiones de Node.js que se destaca por su velocidad y simplicidad1
. Está construido en Rust, lo que le permite ser muy eficiente
. Aquí tienes algunos comandos básicos para usar fnm:

Instalarlo:
```sh
curl -fsSL https://fnm.vercel.app/install | bash
# o
curl -fsSL https://fnm.vercel.app/install | bash -s -- --skip-shell
```
Probe el primero y funcionó.

Para usarlo:
Agrega fnm a tu shell profile: Si estás usando bash, asegurate que esto esta agregado esto al final de tu archivo .bashrc:
.bashhrc esta en la carpeta: C:\Users\jflor

Para bash:
```sh
export PATH=$HOME/.fnm:$PATH
eval "$(fnm env)"

```

Revise y al instalar con curl, el archivo: .bashhrc (ver nota) ya tenia esto:
```sh
# fnm
FNM_PATH="/c/Users/jflor/.local/share/fnm"
if [ -d "$FNM_PATH" ]; then
  export PATH="$FNM_PATH:$PATH"
  eval "`fnm env`"
fi
```
Nota tuve que crear el archivo: .bash_profile en la carpeta raiz del gitBash:
```sh
ir a la raiz de gitbash
cd ~/
```
Si tienes una configuración previa de .bashrc en tu directorio de usuario, puedes incluir los alias y configuraciones allí en lugar de .bash_profile. Sin embargo, .bash_profile es recomendado como ubicación principal para configuraciones de Bash en Windows.


## fnm Fast node manager

permite gestionar diferentes versiones de node

```sh
# recarga tu shell si acabas de instalar:
source ~/.bashrc
# prueba
fnm --version
# instalar una version específica
fnm install 14.17.0
# mostrar las versiones instaladas 
fnm list
# instala la ultima version lts
fnm install --lts
# cambiar a una version específica
fnm use 14.17.0
# usar una versión específica:
fnm use 14.17.0
# pone version de default
fnm default version
# eliminar una versión específica
fnm uninstall 14.17.0
```

## fnm en power shell

Verifica que PowerShell admite winget ejecutando el comando winget --version. Si no lo admite, puedes instalarlo fnm desde el Microsoft Store

```sh
# installs fnm (Fast Node Manager)
winget install Schniz.fnm

# configure fnm environment
fnm env --use-on-cd | Out-String | Invoke-Expression

# download and install Node.js
fnm use --install-if-missing 20

# verifies the right Node.js version is in the environment
node -v # should print `v20.18.0`

# verifies the right npm version is in the environment
npm -v # should print `10.8.2`
```


## bun

Crear proyecto vanilla js

```sh
bun create vanilla
# pej instalar express
bun install express
# ejecutar
bun run dev
```

## pm2

[pm2](https://tecnonucleous.com/2018/03/28/usar-pm2-para-mantener-el-bot-de-telegram-encendido/)

[instalar](https://www.npmjs.com/package/pm2)

```sh
npm install pm2 -g
pm2 list
pm2 start server.js --name alias
pm2 stop alias
pm2 stop serer.js
pm2 stop id
pm2 startup
```

Nota:
Sistema de inicio PM2 no encontrado
PM2, un popular administrador de procesos para aplicaciones Node.js, no es compatible con el sistema de inicio en Windows 10. Esto se debe a que Windows utiliza un sistema de administración de servicios diferente al de Linux, donde PM2 está diseñado para integrarse con el sistema de inicio (por ejemplo, systemd, init.d).

En Windows, PM2 ofrece soluciones alternativas para administrar e iniciar sus aplicaciones Node.js:

Servicio de Windows PM2: puede instalar PM2 como un servicio de Windows mediante pm2-windows-service. Esto le permite administrar PM2 y sus aplicaciones mediante el Administrador de servicios de Windows. Siga las instrucciones de la documentación de PM2 para instalar y configurar el servicio de Windows PM2.
Scripts de inicio: puede crear scripts de inicio personalizados mediante pm2 startup y pm2 stop. Estos scripts se pueden ejecutar manualmente o programar mediante el Programador de tareas de Windows. Consulte la documentación de PM2 para obtener más información.
Bibliotecas de terceros: hay bibliotecas de terceros disponibles, como pm2-logrotate y pm2-windows-startup, que brindan funciones adicionales e integración con Windows. Puede instalar estas bibliotecas mediante npm y configurarlas de acuerdo con su documentación.
En resumen, PM2 no admite el sistema init en Windows 10. En su lugar, puede usar el servicio de Windows de PM2, scripts de inicio personalizados o bibliotecas de terceros para administrar e iniciar sus aplicaciones Node.js en Windows.

## varios

[instalar](https://bun.sh/)
[notas bun](https://www.freecodecamp.org/espanol/news/un-vistazo-rapido-a-bun-1-0-una-alternativa-a-node-js/)
## ligas

[datos falsos](https://gorest.co.in/)
[Ejeemplo manejo de xml](https://blog.logrocket.com/reading-writing-xml-node-js/)
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
<!-- [muy bueno](https://www.arkaitzgarro.com/javascript/capitulo-11.html) -->
[referencia sqlite3 español](https://www.digitalocean.com/community/tutorials/how-to-use-sqlite-with-node-js-on-ubuntu-22-04)
[get, each, all sqlite](https://discuss.codecademy.com/t/why-use-db-each-instead-db-all-or-db-get-in-node-sqlite/381382)

