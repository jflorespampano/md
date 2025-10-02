## promesas

Una [`Promise`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Promise) (promesa en castellano) es un objeto que representa la terminación o el fracaso de una operación asíncrona. La mayoría de las personas consumen `promises` ya creadas, pero también puede crearlas.

### crear promesa

```js
function mipromesa(){
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve("Promesa cumplida");
        }, 3000);
    });
}

mipromesa()
.then(function(resp){
    console.log("promesa exitosa:",resp);
},
function(resp){
    console.log("fracaso la promesa:",resp);
});
```
### ejemplo

Considera la función `crearArchivoAudioAsync()`, la cual genera de manera asíncrona un archivo de sonido de acuerdo a un archivo de configuración, y dos funciones callback, una que es llamada si el archivo de audio es creado satisfactoriamente, y la otra que es llamada si ocurre un error. El código podría verse de la siguiente forma:

```js
function exitoCallback(resultado) {
  console.log("Archivo de audio disponible en la URL " + resultado);
}

function falloCallback(error) {
  console.log("Error generando archivo de audio " + error);
}

crearArchivoAudioAsync(audioConfig, exitoCallback, falloCallback);
```

Usando promesas sería:

```js
crearArchivoAudioAsync(audioConfig).then(exitoCallback, falloCallback);
```

o

```js
const promesa = crearArchivoAudioAsync(audioConfig);
promesa.then(exitoCallback, falloCallback);
```
### Encadenamiento

Suponga que quiere ejecutar varias promesas en forma secuencial

```js
promesa1()
  .then(function (resultado) {
    return promesa2(resultado);
  })
  .then(function (nuevoResultado) {
    return promesa3(nuevoResultado);
  })
  .then(function (resultadoFinal) {
    console.log("Obtenido el resultado final: " + resultadoFinal);
  })
  .catch(falloCallback);
```

```js
promesa1()
  .then((resultado) => promesa2(resultado))
  .then((nuevoResultado) => promesa3(nuevoResultado))
  .then((resultadoFinal) => {
    console.log(`Obtenido el resultado final: ${resultadoFinal}`);
  })
  .catch(falloCallback);
```
### referencias

[Referencia](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Using_promises)
