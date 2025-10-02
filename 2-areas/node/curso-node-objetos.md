---
categoría: programación
tipo: js
---
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

## desestructuración de objetos

```js
const objeto = { propiedadVieja: 'valor', otraPropiedad: 42 };

// Desestructuración con renombrado
const { propiedadVieja: nuevoNombre, otraPropiedad: otroNuevoNombre } = objeto;

console.log(nuevoNombre); // 'valor'
console.log(otroNuevoNombre); // 42
console.log(propiedadVieja); // Error: propiedadVieja is not defined
```
## ejemplo objetos

Un objeto persona:
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

