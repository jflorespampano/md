# Indice
1. [JS](#js)
2. [caracteristicas](#caract)
3. [variables](#variables)
4. [funciones](#funciones)
5. [funciones y this](#fyt)
6. [programacion_funcional](#programacion_funcional)
7. [inmutabilidad](#inmutabilidad)
8. [funciones puras](#funciones_puras)
9. [clases](#clases)
10 [colores en salisa de consola](#colores)

# Nombres de entidades

PascalCase
camelCase
snake_case
kebab-case

# JS <a name="js"></a>

JavaScript (JS) es un lenguaje de programación ligero, interpretado, JavaScript es un lenguaje de programación basada en prototipos, multiparadigma, de un solo hilo, dinámico, con soporte para programación orientada a objetos, imperativa y declarativa (por ejemplo programación funcional). (MDNWeb Docs)

Es soprtado por todos los navegadores y tambien se puede usar del lado del servidor  con NODE.JS. NODE es una plataforma open source para el desarrollo de scripts, servidores, web apps y herramientas de linea de comando.

# caracteristicas de JS <a name="caract"></a>

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

## variables <a name="variables"></a>

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
## Funciones <a name="funciones"></a>

Exsten 2 tipos de funcones: funciones y funciones flecha
```js
//función
function suma(a,b){
    return a+b
}

//función flecha
const resta=(a,b)=>{
    return a-b
}

//funcion anonima
console.log((a,b)=>{
    return a*b
})
//función anonima
console.log(function(a,b){
    return a*b
})

```

## programacion funcional <a name="programacion_funcional"></a>

Aunque js no es un lenguaje con el paradigma funcional, podemos usar algunas herramienntas del lenguaje para escribir programas en este paradigma:

Las herramientas a usar son:
1. Asegurar inmutabilidad de los datos con los que trabaja tu aplicación.
2. Usar funciones puras.
3. Uso de funciones de orden superior.  
4. Uso del currying.
5. Composición de funciones.

### inmutabilidad <a name="inmutabilidad"></a>

Los valores de las variables deben ser inmutables, para lograr esto puede declarar constantes cuando sea posible.
Tambien hay que recordar que las varibles se asignan por valor y los objestos y arreglos se asignan por referencia.
vea objetos e inmutabilidad mas adelante.

### funciones puras <a name="funciones_puras"></a>

Una función pura tiene dos propiedades esenciales:

1. El valor que retorna depende sólo de los argumentos de entrada. O lo que es lo mismo, el valor de retorno no cambiará si los valores de entrada no cambian.
2. No puede modificar nada que este fuera de su ámbito.

**Para lograr esto vea mas adelante el operdor spread**

### currificacion <a name="currificacion"></a>

Currificar consiste en convertir una función de múltiples variables en una secuencia de  funciones unarias

Esto hace que, si la función tiene N argumentos de entrada, nunca se ejecutará si no le proporcionamos todos los argumentos de entrada que pide, al contrario de lo que ocurre por defecto en JavaScript (como con parseInt, que podíamos ejecutarla con un sólo argumento a pesar de recibir dos).

```js
const suma = (a, b) => a + b;

suma(3, 5); //=> 8
suma(3)(5); //=> TypeError

//funcion currificada
const suma = (a) => (b) => a + b;
suma(3)(5); //=> 8
```
### funciones de orden superior <a name="funciones de orden superior"></a>

Las funciones de orden superior son aquellas que reciben una o más funciones como argumento o bien devuelven funciones como resultado. Nos interesan porque nos permiten reutilizar la forma de ejecutar otras funciones. En especial nos serán muy útiles map, filter y reduce, los pilares de la programación funcional en JavaScript, su interés principal está en usarlo sobre arrays.

### composicion de funciones <a name="composición de funciones"></a>

```js
const original = [80, 3, 14, 22, 30];

const result = original
    .filter((value) => value%2 === 0)
    .filter((value) => value > 20)
    .reduce((accumulator, value) => accumulator + value);

console.log(result); // 132
```
en construccion [ver:](https://lemoncode.net/lemoncode-blog/2017/9/5/introduccion-programacion-funcional-javascript)

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

## Objetos en js <a name="objetos"></a>

Crear objetos:
Forma 1 con Object:
```js
var myCar = new Object();
myCar.make = "Ford";
myCar.model = "Mustang";
myCar.year = 1969;

```
Forma 2 usando iniciador de objeto:
```js
var myCar = {
  make: "Ford",
  model: "Mustang",
  year: 1969,
};

```

Forma 3 con funcion constructora:
```js
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}
var mycar = new Car("Eagle", "Talon TSi", 1993);

```

## Se accede a los elementos del objeto así <a name="acceso a elementos en objetos"></a>
```js
myCar.make = "Ford";
myCar.model = "Mustang";
myCar.year = 1969;
//o asi
myCar["make"] = "Ford";
myCar["model"] = "Mustang";
myCar["year"] = 1969;
//Las propiedades no asignadas de un objeto son undefined (y no null).
//por ejemplo para el objeto anterior :
cosole.log(myCar.color); // undefined
```
## ejemplo objetos

Un objeto prsona:
```js
const persona={
    id:0,
    nombre:"andres",
    carrera:"fisica",
    muestra:function(){
        console.log(`id:${this.id} nombre:${this.nombre}`)
    }
}

function fpersona(){
    this.id=0
    this.nombre="rosa"
    this.carrera="mate"
    this.muestra=function(){
        console.log(`id:${this.id} nombre:${this.nombre}`)
    }
}

persona3=new Object()
persona3.id=0
persona3.nombre="teresa"
persona3.carrera="algebra"
persona3.muestra=function(){
    console.log(`id:${this.id} nombre:${this.nombre}`)
}

persona.muestra()
const persona2=new fpersona()
persona2.muestra()
persona3.muestra()
```
Los objetos son asignados a otros objetos por referencia. Esto tiene el efecto que los vuelve mutables, Ejemplo:

```js
//mutabilidad de objetos array
const array=[1,2,3,4,5]
const array2=array
array2[0]=45
console.log(array) //[ 45, 2, 3, 4, 5 ] , sin quererlo mutamos array
console.log(array2) //[ 45, 2, 3, 4, 5 ]
```

### funciones y this <a name="fyt"></a>

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

## inmutabilidad de objetos <a name="inmutabilidad de objetos"></a>

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
## inmutabilidad de arreglos <a name="inmutabilidad de arreglos"></a>

```js
//inmutabilidad con operador spread
const array=[1,2,3,4,5]
const array2=[...array]
array[0]=45
console.log(array) //[ 45, 2, 3, 4, 5 ]
console.log(array2) //[ 1, 2, 3, 4, 5 ]
//map
const arreglo=[2,5,3,7,8,9]
//map --> para cada dato en el arreglo devuelve dato*2
const nvoArreglo=arreglo.map((dato)=>{
    return dato*2
})

//nvoArreglo es un nuevo arreglo donde su i-esimo elemento = i-esimo elemento de arreglo * 2
```
## map <a name="map"></a>

```js
let users = [
    {firstName : "Susan", lastName: "Steward"},
    {firstName : "Daniel", lastName: "Longbottom"},
    {firstName : "Jacob", lastName: "Black"}
  ];
  
  let userFullnames = users.map(function(element){
      return `<li>${element.firstName} ${element.lastName}</li>`;
  })
   const salida=userFullnames.join('\n')
  console.log(userFullnames);
  console.log(salida)
```

## Filter <a name="filter"></a>

```js
var arr = [
    { id: 15 },
    { id: -1 },
    { id: 0 },
    { id: 3 },
    { id: 12.2 },
    {},
    { id: null },
    { id: NaN },
    { id: "undefined" },
  ];
  
  var entradasInvalidas = 0;
  // Si el elemento tiene un atributo id, y su valor correspondiente es un numero
  // Y no es el valor NaN, entonces es una entrada válida
  function filtrarPorID(obj) {
    if ("id" in obj && typeof obj.id === "number" && !isNaN(obj.id)) {
      return true;
    } else {
      entradasInvalidas++;
      return false;
    }
  }
  
  var arrPorID = arr.filter(filtrarPorID);
  
  console.log("Array Filtrado\n", arrPorID);
  // [{ id: 15 }, { id: -1 }, { id: 0 }, { id: 3 }, { id: 12.2 }]
  
  console.log("Número de Entradas Invalidas = ", entradasInvalidas);
  // 4
  
```

## operador coalescencia nula <a name="operador coalescencia nula"></a>

```js
let name = obj.name ?? 'default name';
```
El operador ?? devolverá el lado izquierdo si no es nulo (es decir, nulo o indefinido), de lo contrario, devolverá el lado derecho. Entonces, en el ejemplo anterior, si obj.name no es nulo o indefinido, el nombre se establecerá en obj.name . Pero si obj.name es nulo o indefinido, el nombre será 'nombre predeterminado'.

## inmutabilidad en funciones que manejan objetos <a name="inmutabilidad en funciones que manejan objetos"></a>

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
## ordenar <a name="ordenar"></a>

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

## revertir el arreglo <a name="reverse"></a>

```js
//mutable
usuarios.revserse(); // [{ id: 1}, {id: 2}, {id: 3}]
//inmutable
const inverted = [...usuarios].reverse()
```
## await <a name="await"></a>

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
## solicitar datos get con fetch <a name="get fetch"></a>

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
## enviar formulario con fetch <a name="formulario fetch"></a>

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

## enviar json <a name="enviar json"></a>

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

## clases en js <a name="clases"></a>

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

### extends <a name="extends"></a>

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

Tambien se pueden extender las clases tradicionales basadas en funciones:

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