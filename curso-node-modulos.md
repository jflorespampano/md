# modulos 

Los módulos son la forma en que organizamos nuestro proyecto en diferetes archivos, un nódulo es simplemente un archvo con extensión .js (tambien puede ser extensiones .mjs o .cjs).

Existen 2 formas de trabajar con modulos en node, un modulo es un archivo con código js que puede exportar elementos tales como funciones, clases y objetos.
Las dos formas son:

1. CommonJS que usa la sentencia **require**, archivos con extencion js (o cjs)
2. ESM (ecma script module) que usan la sentencia **import**, archivos con extencion mjs

**Nota CommonJS (es el que usa node por defecto)**

## Modulos CommonJS

Por ejemplo creamos el modulo: operaciones

Archivo:operaciones.js
```js
const suma=(n1,n2)=> n1+n2
const resta=(n1,n2)=> n1-n2
const multiplicacion=(n1,n2)=> n1*n2
const division=(n1,n2)=> n1/n2
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

## Mmodulos ESM (Ecma Script odule)

Para usar el sistema module ESM, los archivos tendran la extension .mjs o pueden tener extencion .js y tener la entrada "type":"module" en el package.json.

### Exportar/importar en ESM:

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

## Resumen de sintaxis de ESM

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