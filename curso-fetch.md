# fetch 

## promesas
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

El método fetch() lanza el proceso de solicitud de un recurso de la red. Esto devuelve una promesa que resuelve al objeto Response que representa la respuesta a la solicitud realizada.

## Formato general

```js
fetch(url, {
    method: "POST", // *GET, POST, PUT, DELETE, etc.
    mode: "cors", // no-cors, *cors, same-origin
    cache: "no-cache", // *default, no-cache, reload, force-cache, only-if-cached
    credentials: "same-origin", // include, *same-origin, omit
    headers: {
      "Content-Type": "application/json",
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    redirect: "follow", // manual, *follow, error
    referrerPolicy: "no-referrer", // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    body: JSON.stringify(data), // // el tipo de datos del body debe coincidir cpn el header "Content-Type"
})
```

No usaremos todas las opciones, las que usaremos son:(method,headers,body) en algunas ocaciones(mode).

## Formato con promesas

```js
function postData(url = "", data = {}) {
    // Default options are marked with *
    return fetch(url, {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(data)
    })
    .then(respuesta=>{
        if(respuesta.ok){
            return respuesta.json()
        }else{
            throw new Error("Error al cargar")
        }
    })
}
const album={
    "userId": 1,
    "title": "quidem molestiae enim"
}
postData("https://jsonplaceholder.typicode.com/albums", album)
.then((data) => {
  console.log(data); 
});
```
## Formato con async/await

```js
// Example POST method implementation with await:
async function postData(url = "", data = {}) {
  // Default options are marked with *
  const response = await fetch(url, {
    method: "POST", // *GET, POST, PUT, DELETE, etc.
    headers: {
      "Content-Type": "application/json",
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    body: JSON.stringify(data), // body data type must match "Content-Type" header
  })
  return response.json(); // parses JSON response into native JavaScript objects
}

const album={
    "userId": 1,
    "title": "quidem molestiae enim"
}
postData("https://jsonplaceholder.typicode.com/albums", album)
.then((data) => {
  console.log(data); 
});

```

# Ejemplos

## solicitar recurso get

```js
//solicitar datos con get
const url="http://localhost:3000"
let request = new Request(url,
    {
        method: 'get',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' }
    });
    fetch(request)
    .then(function (returnedValue) {
        if (returnedValue.ok) {
            return returnedValue.json()
        } else {
            console.log("no se pudo recuperar los datos")
            return Promise.reject("no se pudo recuerar datos")
        }
    })
    .then((data)=>{
        //hacer algo con los datos
        console.log("Datos en formato json",data)
    })
    .catch(function (err) {
        console.error(err);
    })
```
//como el get es el default:
```js
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
//opcion con async/await
```js
const leerdatos=async(url)=>{
    try {
        const response=await fetch(url)
        if(!response.ok){throw new Error("Erron en los datos")}
        const data=await response.json()
        console.log(data)
    } catch (error) {
        console.log("Eror:",error)
    }
}
leerdatos('https://jsonplaceholder.typicode.com/posts')
```
## enviar datos post ejemplo 1

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
});
.catch(function (err) {
    console.error(err);
})
```

## enviar datos post indicando formato de los datos
```js
//enviar datos de un formulario
const data = new FormData(document.getElementById('miformulario'));
fetch(url, {
    method: 'post',
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
    },
    body: new URLSearchParams(data)
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

## Enviar json

```js
//poner en el header
headers: {
    "Content-Type": "application/json",
}
// y en el body
body: JSON.stringify(Object.fromEntries(new FormData(document.getElementById('miformulario'))))
```

Que explicado hace lo siguiente

1. Obtener los datos del formulario:

```js
const formulario=new FormData(document.getElementById('miformulario'))
```

2. Crear un objeto js a partir del formulario:

```js
const obj=Object.fromEntries(formulario)
```

3. Convertirlo a json

```js
JSON.stringify(obj)
```
Ejemplo:

```js
//enviar datos de un formulario
// const data = new FormData(document.getElementById('miformulario'));
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
# fetch usando async await

POST:

```js
document.getElementById("btn_enviar").onclick = async function(event){
    event.preventDefault();
    try {
        const data=await fetch('recibePOST.php', {
            method: 'post',
            body: new FormData(document.getElementById('frm_trabajo'))
        })
        const txt=await data.text()
        document.write('recibo de regreso: ',txt);
    } catch (error) {
        document.write('Error: ',error);
    }
        
};
```

GET:

```js
document.getElementById("btn_enviar").onclick = async function(event){
    event.preventDefault();
    let movimiento=document.getElementById("txt_movimiento").value+"01";
    let id=document.getElementById("txt_id").value;
    let nombre=document.getElementById("txt_nombre").value+"01";
    let apellido=document.getElementById("txt_apellido").value;
    let parametros="?movimiento="+movimiento+"&id="+id+"&nombre="+nombre+"&apellido="+apellido;
    //var request = new Request('recibeGET.php?movimiento=1&id=1&nombre=luisa&apellido=rosales&edad=4', 
    let request = new Request('recibeGET.php'+parametros, 
    {
        method: 'get',
        headers: {'Content-Type':'application/x-www-form-urlencoded'}
    });
    try {
        const data=await fetch(request)
        const txt=await data.text()
        if(data.ok){
            document.write('Ok recibo de regreso: ',txt);
        }else{
            document.write('Error : ',txt);
        }
    } catch (error) {
        document.write("error en la solicitud "+error)
    }
    
}
```

Para ´probar el fetch puesde usar el sitio: `http://mock.codes/` que devuelve el error que indicas, por ejemplo: `http://mock.codes/500` te responde con error HTTP 500.
## Ligas
[api fetch](https://developer.mozilla.org/es/docs/Web/API/fetch)

[Usando fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

[fromEntries](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries)

[Referencia en español](https://es.javascript.info/fetch-api)