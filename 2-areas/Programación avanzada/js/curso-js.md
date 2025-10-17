---
categoría: programación
tipo: js
---

# Índice

1. [[curso-js#caracteristicas de JS]]
2. [[curso-js#variables]]
3. [[curso-js#Funciones]]
4. [[curso-js#Parámetros]]
5. [[curso-js#Objetos en js]]
6. [[curso-js#desestructuración de objetos]]
7. [[curso-js#arreglos]]
8. [[curso-js#operador coalescencia nula]]
9. [[curso-js#funciones y this]]
10. [[curso-js#inmutabilidad en funciones que manejan objetos]]
11. [[curso-js#programacion funcional]]


# Nombres de entidades

PascalCase
camelCase
snake_case
kebab-case

# JS

JavaScript (JS) es un lenguaje de programación ligero, interpretado, JavaScript es un lenguaje de programación basada en prototipos, multiparadigma, de un solo hilo, dinámico, con soporte para programación orientada a objetos, imperativa y declarativa (por ejemplo programación funcional). (MDNWeb Docs)

Es soportado por todos los navegadores y también se puede usar del lado del servidor  con NODE.JS. NODE es una plataforma open source para el desarrollo de scripts, servidores, web apps y herramientas de liínea de comando.

# características de JS

1. Imperativo: JavaScript es un lenguaje imperativo, es decir, se ejecutan las sentencias de manera secuencial.

2. Tipado débil: En JavaScript, no se define el tipo de una variable al instanciarla. El tipo de la variable se asigna según el valor que se le asigna. Además, si se cambia el valor asignado a la variable, esta puede cambiar su tipo de datos.

3. Interpretado: JavaScript no se compila en código máquina. En su lugar, necesita un intérprete para ejecutarse. Sin embargo, motores como Chrome V8 realizan compilaciones JIT (Just-In-Time) para mejorar el rendimiento.

4. Sencillo: JavaScript es un lenguaje fácil de aprender y utilizar, no requiere conocimientos avanzados de programación para desarrollar aplicaciones.

5. Cliente y servidor: JavaScript puede ser utilizado tanto para desarrollo de aplicaciones del lado cliente (front-end) como del lado servidor (back-end) mediante tecnologías como Node.js.

6. Orientado a objetos: Aunque no es un lenguaje puro de programación orientada a objetos como C++ o Java, JavaScript utiliza prototipos para definir objetos y permite la creación de objetos y herencia de propiedades.

7. Multiplataforma: JavaScript se ejecuta en diferentes navegadores (Google Chrome, Microsoft Edge, Safari, Opera, etc.) y sistemas operativos (Windows, Mac, Linux, etc.).

8. Compatibilidad: JavaScript es compatible con la mayoría de los navegadores web modernos y se ejecuta directamente en el navegador del usuario final.

9. Extensibilidad: Existen diferentes frameworks y bibliotecas de JavaScript que permiten ampliar las funcionalidades del lenguaje y facilitar el desarrollo de aplicaciones.

10. Evolutivo: JavaScript es un lenguaje en constante evolución, con nuevas características y mejoras constantemente agregadas a los navegadores y frameworks.

A continuación un resumen del lenguaje.

## tipo de datos

El último estándar ECMAScript define nueve tipos:

Seis tipos de datos primitivos, controlados por el operador typeof

1. Undefined: typeof instance === "undefined"
2. Boolean: typeof instance === "boolean"
3. Number: typeof instance === "number"
4. String: typeof instance === "string"
5. BigInt: typeof instance === "bigint"
6. Symbol: typeof instance === "symbol"
7. Null: typeof instance === "object". Tipo primitivo especial. En JavaScript, null es un valor primitivo que representa la ausencia intencional de cualquier valor u objeto. Es decir, se utiliza para indicar que una variable no tiene ningún valor asignado de forma deliberada. Aunque null es un primitivo, curiosamente, su tipo (typeof) es "object" debido a un error histórico en JavaScript.

8. Object: typeof instance === "object". Tipo estructural especial que no es de datos pero para cualquier instancia de objeto construido que también se utiliza como estructuras de datos: new Object, new Array, new Map, new Set, new WeakMap, new WeakSet, new Date y casi todo lo hecho con la palabra clave new;

9. Function: una estructura sin datos, aunque también responde al operador typeof: typeof instance === "function". Esta simplemente es una forma abreviada para funciones, aunque cada constructor de funciones se deriva del constructor Object.

## variables

Como js es un lenguaje debilmente tipado, las variables no tienen tipo asignado en la declaración, se declaran así:

```js
var saludo="hola"
const x=0
let nombre=true
//tipos primitivos se asignacion por valor
int x=0
iny y=x
x=2
console.log(x) //2
console.log(y) //0

//los objetos se asignan por referencia
//declaramos un objeto
let persona={
    "nombre": "Juan",
    "edad": 30
}

//al copiar, copia la referencia
let persona2=persona;
persona2.nombre="Pedro";

console.log("persona:",persona) // persona:{ nombre: 'Pedro', edad: 30 }
console.log("persona 2:",persona2) // persona2:{ nombre: 'Pedro', edad: 30 }

//si queremos crear un clon:
//declaramos un objeto
let persona={
    "nombre": "Juan",
    "edad": 30
}

//clonamos el objeto
let persona3={...persona};
persona3.nombre="Luis";

console.log("persona:",persona) // persona:{ nombre: 'Juan', edad: 30 }
console.log("persona 3:",persona3) // persona2:{ nombre: 'Luis', edad: 30 }

//usar const para inmutabilidad 
const nombre="juan perez"
nombre="maria uc" //error

```
## Funciones

![[curso-node-funciones]]


## json

JSON (acrónimo de JavaScript Object Notation, 'notación de objeto de JavaScript') es un formato de texto sencillo para el intercambio de datos. Se trata de un subconjunto de la notación literal de objetos de JavaScript, aunque, debido a su amplia adopción como alternativa a XML, se considera un formato independiente del lenguaje.


```js
//objeto en js
const persona={
  id:34,
  nombre:"Andrea",
  ap:"Flores",
  am:"Sanchez",
  sexo:"f",
  carrera:"ISC",
  edad:19,
  matricula:"244534",
  activo:'si'
}

console.log(persona)
//json en js
console.log(JSON.stringify(persona))
```

## Objetos en js

![[curso-node-objetos]]


## arreglos

![[curso-node-arreglos]]
### funciones y this

En una funcion el valor de this está determinado por cómo se invoca a la función. No puede ser establecida mediante una asignación en tiempo de ejecución

El this en una funcion flecha es siempre el del contexto léxico que envuelve a la función.

En el contexto de ejecución global (fuera de cualquier función), this se refiere al objeto global, ya sea en modo estricto o no.
```js
console.log(this.document === document); // true

// En los navegadores web, el objeto window también es un objeto global:
console.log(this === window); // true

this.a = 37;
console.log(window.a); // 37
```

Dentro de una función, el valor de this depende de cómo la función es llamada.

En una llamada simple:
```js
function f1() {
  return this;
}
f1() === window; // objeto global

//
function f2() {
  "use strict"; // consultar modo estricto
  return this;
}
f2() === undefined;
```

Cuando es llamada con el operador dot(punto), el this toma el contexto del objeto que precede al punto
```js
var o = {
  prop: 37,
  f: function () {
    return this.prop;
  },
};

console.log(o.f()); // logs 37
//como la funcion f es llamada con o. su contexto es el objeto o y this se refiere al ambito del objeto o
```

Para ver que el comportamiento depende de como la funcion es llamada pruebe esto:

```js
var o = { prop: 37 };

function independent() {
  return this.prop;
}

o.f = independent;

console.log(o.f()); // logs 37
console.log(independent()); //logs  undefined //prop esta indefinido

//el primer connsole.log llama a la funcon independet por medio  de o.f(), por tanto el this es el de el contexto lexico de o
//en el segundo console.log la funcion independent se llama directamente, 
//por  lo tanto no tiene un contexto lexico asociado y this esta indefinido
```

## inmutabilidad de objetos

Suponga que tiene el objeto persona:

```js
const persona={
    id:0,
    nombre:"andres",
    carrera:"fisica",
    muestra:function(){
        console.log(`id:${this.id} nombre:${this.nombre}`)
    }
}

//para garantizar la inmutabilidad debemos crear persona2 con el operador spread (...), 
//este operador hace una copia del objeto dado
const persona2={...persona,calificacion:90} //clonamos el objeto1 y le agregamos un nuevo campo
persona.id=2
persona.nombre="andrea"
persona.muestra() //muestra el objeto original
persona2.muestra() //muestra un nuevo objeto con un campo calificacion  agregado
```

## operador coalescencia nula

```js
let name = obj.name ?? 'default name';
```
El operador ?? devolverá el lado izquierdo si no es nulo (es decir, nulo o indefinido), de lo contrario, devolverá el lado derecho. Entonces, en el ejemplo anterior, si obj.name no es nulo o indefinido, el nombre se establecerá en obj.name . Pero si obj.name es nulo o indefinido, el nombre será 'nombre predeterminado'.

## inmutabilidad en funciones que manejan objetos

```js
const usuarios = [
	{ 
		id: 1,
		name: "brad gibson",
		email: "brad.gibson@example.com"
	},
	{
		id: 2,
		name: "Kuzey Karaduman",
		email: "kuzey.karaduman@example.com"
	},
	{
		id: 3,
		name: "Heinz-Werner Konrad",
		email: "heinz-werner.konrad@example.com"
	}
]
function agregaUsuario(usuarios){
    const newUser = {
        id:4,
        name: "Stephen Watkins",
        email: "stephen.watkings@example.com"
    }
    //usar push modifica el arreglo original
    //usuarios.push(newUser) // [{ id: 1}, {id:2}, {id: 3}, { id: 4} ]
    //para lograr la inmutabilidad usar spread
    const newUsuarios = [...usuarios, newUser ]
    retrun newUsuarios
}

const usuarios2=agregaUsuario(usuarios)

```

Para este mismo ejemplo si queremos insertar el usuario enmedio
```js
const newUsuarios = [...usuarios.slice(0,1), newUser, ...usuarios.slice(3)]
```
## ordenar

```js
//mutable
function compare(a, b) {
  if(a.id > b.id) {
    return -1
  }
	if(a.id < b.id) {
		return 1
	}
  return 0
}
usuarios.sort(compare); // [{ id: 3}, {id: 2}, {id: 1}]
//inmutable
const sorted = [...usuarios].sort(compare)
```

## revertir el arreglo

```js
//mutable
usuarios.revserse(); // [{ id: 1}, {id: 2}, {id: 3}]
//inmutable
const inverted = [...usuarios].reverse()
```
## await

```js
const leerDatos=async ()=>{
    const resp=await fetch('https://jsonplaceholder.typicode.com/posts')
    const data= await resp.json()
    return data
}

async function procesaDatos(){
    const data=await leerDatos()
    const dm=data.map(d=>{
        return(
            {
                "id":d.id,
                "title":d.title
            }
        )
    })
    console.log(dm)
}

procesaDatos()

```
## solicitar datos get con fetch

```js
const url='https://jsonplaceholder.typicode.com/posts'
fetch(url)
.then(function(response) {
    if(!response.ok){throw new Error("Error al recibir datos")}
    return response.json();
})
.then((data)=> {
    console.log('data = ', data);
    data.forEach((x)=>{
        ...
    })
})
.catch(function(err) {
    console.log("Error...");
    console.error(err);
});

```

//ejemplo solicitar datos con get usando async/await
```js
const leerdatos=async(url)=>{
    try {
        const response=await fetch(url)
        if(!response.ok){throw new Error("Error en los datos")}
        const data=await response.json()
        console.log(data)
    } catch (error) {
        console.log("Eror:",error)
    }
}
leerdatos('https://jsonplaceholder.typicode.com/posts')
```
## enviar formulario con fetch

```js
//enviar datos de un formulario
const data = new FormData(document.getElementById('miformulario'));
fetch(url, {
    method: 'post',
    body: data
})
.then(function (response) {
    if (response.ok) {
        return response.text()
    } else {
        console.log("no se pudieron actualizar los datos")
        return Promise.reject("no se pudo insertar el dato")
    }
})
.then(resp => {
    console.log(resp);
})
.catch(function (err) {
    console.error(err);
})
```

En el código anterior, en el fetch, **no** se indica un **head** con la especificacion del formato en que se envian los datos, por que por default el fromato es <span style="color:yellow;">'Content-Type: application/x-www-form-urlencoded' </span>, aunque tambien se podria poner así:

```js
fetch(url, {
    method: 'post',
    headers: {
        "Content-Type": "application/x-www-form-urlencoded",
    }
    body: data
})
```

## enviar json

```js
//Tomar datos de un formulario y enviarlos en formato json
const frm=document.getElementById('miformulario')
//const frm=document.querySelector("#miformulario")
const data = new FormData(frm);
const datajson=Object.fromEntries(data)
fetch(url, {
    method: 'post',
    headers: {
        "Content-Type": "application/json",
    },
    body: JSON.stringify(datajson)
})
.then(function (response) {
    if (response.ok) {
        return response.text()
    } else {
        console.log("no se pudieron actualizar los datos")
        return Promise.reject("no se pudo insertar el dato")
    }
})
.then(resp => {
    console.log(resp);
});
.catch(function (err) {
    console.error(err);
})
```

En el ejemplo anterior como el formato en que deseamos enviar es json y no es el formato default, debemos especificar un encabezzado que indique que los datos los enviamos en formato json.

Ejemplo:
```js
//enviar datos de un formulario, hay varias formas:
//1:tomar datos de un formulario
// const data = new FormData(document.getElementById('miformulario'));
//2:o en su defecto tomarlos directamente de un objeto
// const objData={"userId":"11","title":"mi titulo","body":"nuevo body"}
//3:o crear un FormData y asignar los datos direcctamente y a partir de ahi consttruir un objeto
//usando fromEntries
const data = new FormData()
data.append("userId","11")
data.append("title","mi titulo")
data.append("body","nuvo body")
const objData=Object.fromEntries(data)
fetch('https://jsonplaceholder.typicode.com/posts', {
    method: 'POST',
    body: JSON.stringify(objData),
    headers: {
      'Content-type': 'application/json; charset=UTF-8',
    },
  })
.then((response) => response.json())
.then((json) => console.log(json));
```

Ejemplo con async/await
```js
// const data = new FormData(document.getElementById('miformulario'));
const data = new FormData()
data.append("userId","11")
data.append("title","mi titulo")
data.append("body","nuvo body")
const objData=Object.fromEntries(data)
//
const envia=(url,objData)=>{
    try {
        const response=fetch(url, {
            method: 'POST',
            body: JSON.stringify(objData),
            headers: {
            'Content-type': 'application/json; charset=UTF-8',
            },
        })
        if(!response.ok){throw new Error("Erro en los datos")}
        const data=await response.json()
        console.log(data)
    } catch (error) {
        console.log("Eror:",error)
    }
}
envia('https://jsonplaceholder.typicode.com/posts',objData)
```

## clases en js

Azucar sintactica para la creación de objetos en js
```js
class Persona{
    #id 
    #nombre 
    constructor(id,nombre){
        this.#id=id
        this.#nombre=nombre
    }
    get nombre(){
        return this.#nombre
    }
    set nombre(nuevo){
        this.#nombre=nuevo
    }
}

const p=new Persona(4,"juana")
p.nombre="rosa"
console.log(p.nombre)
```

### extends

```js
class Animal {
  constructor(nombre) {
    this.nombre = nombre;
  }

  hablar() {
    console.log(this.nombre + " hace un ruido.");
  }
}

class Perro extends Animal {
  hablar() {
    console.log(this.nombre + " ladra.");
  }
}

```

También se pueden extender las clases tradicionales basadas en funciones:

```js
function Animal(nombre) {
  this.nombre = nombre;
}
Animal.prototype.hablar = function () {
  console.log(this.nombre + "hace un ruido.");
};

class Perro extends Animal {
  hablar() {
    super.hablar();
    console.log(this.nombre + " ladra.");
  }
}

var p = new Perro("Mitzie");
p.hablar();

```
Fijarse que las clases no pueden extender objectos regulares (literales). Si se quiere heredar de un objecto regular, se debe user Object.setPrototypeOf()::

### super

```js
class Gato {
  constructor(nombre) {
    this.nombre = nombre;
  }

  hablar() {
    console.log(this.nombre + ' hace ruido.');
  }
}

class Leon extends Gato {
  hablar() {
    super.hablar();
    console.log(this.nombre + ' maulla.');
  }
}

```

### clases abstractas

```js
class Persona{
  #id
  #nombre
  #correo
  constructor(id='',nombre='',correo=''){
    if(new.target === Persona){
      throw new Error("No se puede instancia esta clase")
    }
    this.id=id
    this.nombre=nombre
    this.correo=correo
  }
  muestra(){
    throw new Error("Este método debe ser implementado")
  }
}
class alumno extends Persona{
  muestra(){
    console.log(`id:${this.id}, nombre:${this.nombre}, correo:${this.correo}`)
  }
}

const p=new alumno(1,'ana','@mail')
p.muestra()
```

## iteradores

```js
function* fibonaci(){
  let x1=1;
  let x2=0;
  for(;true;){
      xs=x1+x2
      x1=x2
      x2=xs
      yield xs
    
  }
}
const f=fibonaci()
console.log(f.next())
console.log(f.next())
console.log(f.next())
console.log(f.next())
console.log(f.next())

```

salida:

{value: 1, done: false}
{value: 1, done: false}
{value: 2, done: false}
{value: 3, done: false}
{value: 5, done: false}

## referencias

[clases](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Classes)