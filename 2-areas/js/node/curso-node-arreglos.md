---
categoría: programación
tipo: node
tags:
  - array
---

## declarando arreglos

```js
// Usando el constructor Array
let arr1 = new Array(1, 2, 3);

// Usando la notación literal (recomendada)
let arr2 = [1, 2, 3];
```

## acceso a elementos

```js
let frutas = ['manzana', 'banana', 'cereza'];
console.log(frutas[0]); // 'manzana'
```

## push pop

```js
let arr = [1, 2, 3];
arr.push(4); // [1, 2, 3, 4]
arr.pop();   // [1, 2, 3]
arr.unshift(0); // [0, 1, 2, 3]
arr.shift(); // [1, 2, 3]
```

## longitud

```js
let arr = [1, 2, 3];
console.log(arr.length); // 3
```

## inmutabilidad de arreglos

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
## map

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

## Filter

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

## reduce

```js
array.reduce(
    callback(acumulador, valorActual[, indice[, array]]), valorInicial
)

const array = [1, 2, 3, 4];
const valorInicial = 0;
const suma = array.reduce((acumulador, valorActual) => {
  return acumulador + valorActual;
}, valorInicial); // Resultado: 10
```
## forEach

```js
array.forEach(function(elemento, indice, array) {
  // código a ejecutar por cada elemento
});
```
```js
const frutas = ['manzana', 'banana', 'naranja'];

frutas.forEach(function(fruta) {
  console.log(fruta);
});
// Salida:
// manzana
// banana
// naranja
```
