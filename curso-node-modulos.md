# modulos 

Los módulos son la forma en que organizamos nuestro proyecto en diferetes archivos, un módulo es simplemente un archvo con extensión .js (tambien puede ser extensiones .mjs o .cjs).

Un modulo es un archivo con código js que puede exportar elementos tales como funciones, clases y objetos. Existen 2 formas de trabajar con modulos en node, Las dos formas son:

1. CommonJS que usa la sentencia **const id=require('archivo.cjs')** para importar, y **module.exports={}** para exportar, requiere archivos con extencion js (o cjs)
2. ESM (Ecma Script Module) que usa la sentencia **import id from 'archivo.mjs'** para importar, y **export {}/export default funcion** para exportar, archivos con extencion mjs

**Nota CommonJS (es el que usa node por defecto)**

## Modulos CommonJS

Por ejemplo creamos el modulo: operaciones

Archivo:**operaciones.js**
```js
const suma=(n1,n2)=> n1+n2
const resta=(n1,n2)=> n1-n2
const multiplicacion=(n1,n2)=> n1*n2
const division=(n1,n2)=> n1/n2
module.exports={suma, resta, multiplicacion, division}
```

En el archivo **main.js**
```js
//importar el modulo
const operaciones = require('./operaciones.cjs')
console.log(operaciones.suma(2,3))
```

**Nota**: Con require se puede importar un archivo json, el archivo json no deberá tener module.exports

## Usar commonjs en un proyecto

Se puede definir en el proyecto el tipo de modulos a usar (commonjs o esm), en el archivo package.json (creado con el comando npm init):

* para definir que se usará Commonjs, en el archivo package.json, no poner nada o poner la entrada: 
**"type":"commonjs"**
* para usar modulos de tipo ESM poner la entrada: 
**"type":"module"**

## Modulos ESM (Ecma Script Module)

Para usar el sistema module ESM, los archivos tendran la extension .mjs o pueden tener extencion .js y tener la entrada "type":"module" en el package.json.

### Exportar/importar en ESM:

Archivo: operaciones.mjs
```js
const suma=(n1,n2)=> n1+n2
const resta=(n1,n2)=> n1-n2
const multiplicacion=(n1,n2)=> n1*n2
const division=(n1,n2)=> n1/n2

export {suma, resta, multiplicacion, division}
export default suma
```
Otra forma de escribir un archivo operaciones.mjs
```js
export const data=[
    {name:"ana"},
    {name:"luis"},
    {name:"paco"},
    {name:"sergio"},
    {name:"rosa"}
]
export const suma=(n1,n2)=>  n1+n2
export const resta=(n1,n2)=> n1-n2
export const multiplicacion=(n1,n2)=> n1*n2
export const division=(n1,n2)=> n1/n2
export default suma
```
Para importarlo

en el main.js
```js
//importar desestructurando
import {suma, resta, multiplicacion, division} from './operacines.mjs'
// y llamar así: suma(_,_)
//o importar el default
import suma from './operacines.mjs'
// y llamar así: suma(_,_)
//o
import * as operaciones from './operacines.mjs'
// y llamar así: operaciones.suma(_,_)
```

## Resumen de sintaxis de ESM

|                    Uso                      |              sintaxis               |
|---------------------------------------------|-------------------------------------|
|importar un modulo completo                  | import * as name from ‘module-name’ |
|importar el export default de 1 modulo       | import name from ‘module-name’      |
|importar una exportacion unica               | import { name } from ‘module-name’  |
|importar multiples exportaciones             | import { nameOne , nameTwo } from ‘module-name’ |
|importar un modulo solo para efectos laterales| import ‘./module-name’              |


## Cambios según el tipo de modulos

### En common js
En commonjs puede usar las variables predefiniidas: __dirname, __filename. __filename contiene el nombre del archivo en ejecución con su ruta absoluta, __dirname contiene solo la ruta.

```js
console.log(__dirname);
console.log(__filename);
```

###  En ESM

En ESM no se puede importar archivos json, tampoco se puede usar el __dirname, ni el __filename.
Para hacerlo, hay que saber que el import es un objeto:

import.meta.url es una propiedad del objeto import.meta en Node.js, que devuelve la URL del archivo del módulo actual. Esta propiedad forma parte de la especificación ECMAScript para módulos y está implementada en Node.js.

El método fileURLToPath en Node.js es parte de la clase URL, que se utiliza para convertir una cadena de URL de archivo o un objeto URL en una ruta codificada correctamente. Este método garantiza que los caracteres codificados en porcentaje se decodifiquen de manera absoluta y que la ruta resultante sea válida en todas las plataformas.


Crear las variabes __dirname, __filename en ESM
```js
import * as url from 'url';
const __filename = url.fileURLToPath(import.meta.url);
const __dirname = url.fileURLToPath(new URL('.', import.meta.url));

console.log("path",__dirname)
console.log("file",__filename)
```

### Uso  de cwd()

process.cwd() es un método de Node.js que devuelve el directorio de trabajo actual del proceso de Node.js. Proporciona la ruta absoluta del directorio desde el que se inició el proceso de Node.js. Este directorio se suele denominar “directorio de trabajo actual” o “CWD” "Current Work Directory"

```js
process.cwd() //devuelve el directorio de trabajo corriente del proceso de Node.js
```
La diferencia con __dirname y cwd() es que __dirname devuelve el directorio del archivo actual en ejecución y cwd() devuelve el directorio de inicio del proyecto. 

### Usar path.join()

Para construir rutas y unir todos los segmentos empleando el separador específico de la plataforma, utilizamos el método join. Este método no solo une los segmentos, sino que también normaliza el resultado según la plataforma en la que se esté ejecutando el código. join se encarga de manejar los detalles específicos de la plataforma, asegurando que la ruta resultante sea coherente y compatible independientemente del sistema operativo.

En ESM
```js
import {join} from 'node:path'
const mipath=join(process.cwd(),'js')
console.log("mi path:",mipath)
```

Otra forma:
```js
import path from 'node:path'
const mipath=path.join(process.cwd(),'js')
console.log("Mi path:",mipath)
```

En Common module
```js
const path = require('path');
const joinedPath = path.join('/foo', 'bar', 'baz/asdf');
console.log(joinedPath); // Output: "/foo/bar/baz/asdf"
```

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
otra forma:
```js
import('./opsmjs.mjs')
.then(({suma})=>{
    console.log(suma(4,5))
})
```

### ejemplo crear servidor express con modulos ESM

```js
//index.js

import express from 'express';
const app = express();

app.get('/', (req, res) => {
	res.send('GeeksforGeeks');
})
const PORT = 5000;

app.listen(PORT, () => {
	console.log(`Running on PORT ${PORT}`);
})

```


## notas


## Refs

[desde youtube: desarrollo Util]