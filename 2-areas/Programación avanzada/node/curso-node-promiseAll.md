## Promesas

### promise.all

Promise.all se cumple cuando todas las promesas del iterable dado se han cumplido, o es rechazada si alguna promesa no se cumple.

Promise.all Devuelve una promesa que se resuelve cuando todas las promesas en la matriz de entrada se han resuelto correctamente.
Si alguna de las promesas se rechaza, la promesa devuelta se rechaza inmediatamente, con el primer motivo de rechazo.
El orden de las promesas resueltas se conserva, siguiendo el orden de la matriz de entrada.

Promise.allSettled():

Devuelve una matriz de objetos, cada uno de los cuales representa el estado de una promesa en la matriz de entrada.
Cada objeto contiene una propiedad de estado que indica si la promesa se resolvió ('cumplida') o se rechazó ('rechazada'), junto con una propiedad de valor que contiene el resultado (si se resolvió) o el motivo del rechazo (si se rechazó).
El orden de los objetos en la matriz devuelta coincide con el orden de las promesas de entrada.

Ejemplo:

Suponga las promesas:
```js
const p1=(mensaje)=>{
    return new Promise((resolve,reject)=>{
        setTimeout(() => {
            resolve(mensaje)
        }, 4000);
    })
}
const p2=(mensaje)=>{
    return new Promise((resolve,reject)=>{
        setTimeout(() => {
            resolve(mensaje)
        }, 4000);
    })
}
const p3=(mensaje)=>{
    return new Promise((resolve,reject)=>{
        setTimeout(() => {
            resolve(mensaje)
        }, 4000);
    })
}
const p4=(mensaje)=>{
    return new Promise((resolve,reject)=>{
        setTimeout(() => {
            reject(mensaje)
        }, 4000);
    })
}

const promesas=[p1("Promesa 1"),p2("Promesa 2"),p3("Promesa 3"),p4("Promesa 4")]

```
Promise.all()
```js
Promise.all(promesas)
.then(resp=>{
    console.log("respuesta:",resp)
})
.catch(err=>{
    console.log("Error:",err)
})
```
Salida:
si en la promesa 4 ejecuta el reject() como se muestra en el código:

Error: Promesa 4

Si en la prommesa 4 sustituye el reject por resolve()

Salida:
respuesta: [ 'Promesa 1', 'Promesa 2', 'Promesa 3', 'Promesa 4' ]


Promise.allSettled()
```js
Promise.allSettled(promesas)
.then(resp=>{
    console.log("respuesta:",resp)
})
.catch(err=>{
    console.log("Error:",err)
})
```

Salida;
```json
respuesta: [
  { status: 'fulfilled', value: 'Promesa 1' },
  { status: 'fulfilled', value: 'Promesa 2' },
  { status: 'fulfilled', value: 'Promesa 3' },
  { status: 'rejected', reason: 'Promesa 4' }
]

```
