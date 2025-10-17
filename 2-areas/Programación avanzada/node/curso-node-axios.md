## axios

[Axios](https://axios-http.com/es/docs/example)
## Instalación

```sh
npm install axios
```
```html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
```

ejemplo:
```js
const axios = require('axios');

// Hacer una petición para un usuario con ID especifico
axios.get('/user?ID=12345')
  .then(function (response) {
    // manejar respuesta exitosa
    console.log(response);
  })
  .catch(function (error) {
    // manejar error
    console.log(error);
  })
  .finally(function () {
    // siempre sera executado
  });

// Opcionalmente, la solicitud anterior también se puede realizar como
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
  .finally(function () {
    // siempre sera ejecutado
  });  

// ¿Quieres usar async/await? Añade la palabra reservada `async` a tu función/método externo.
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```

## axios post

Axios envía datos como JSON por defecto (no necesita headers ni JSON.stringify). **Axios se encarga de Serializar el objeto JavaScript** a una cadena JSON. **Establece el `Content-Type`** en `application/json` en los headers de la solicitud.

```js
axios.post('https://api.example.com/data', { user: 'John' })
  .then(response => console.log(response.data));
```

```js
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```


## ejemplo

```html
<form id="myForm">
  <input type="text" name="usuario" placeholder="Usuario">
  <input type="password" name="contraseña" placeholder="Contraseña">
  <button type="submit">Enviar</button>
</form>
```

```js
document.getElementById("myForm").addEventListener("submit", async (e) => {
  e.preventDefault(); // Evita el envío tradicional

  // e.target es el elemento que genero el evento, en este caso el form
  // 1. Obtener datos del formulario con FormData
  const formData = new FormData(e.target);

  // 2. Convertir FormData a un objeto JavaScript
  const formDataObj = Object.fromEntries(formData.entries());

  // 3. Enviar con Axios (POST como JSON)
  try {
    const response = await axios.post("https://tu-api.com/endpoint", formDataObj);
    console.log("Respuesta del servidor:", response.data);
    alert("¡Datos enviados correctamente!");
  } catch (error) {
    console.error("Error al enviar:", error.response?.data || error.message);
    alert("Error al enviar el formulario.");
  }
});
```

## peticiones concurrentes

```js
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

Promise.all([getUserAccount(), getUserPermissions()])
  .then(function (results) {
    const acct = results[0];
    const perm = results[1];
  });
```

## axios.delete

```js
// Simple DELETE request with axios
const element = document.querySelector('#delete-request .status');
axios.delete('https://reqres.in/api/posts/1')
.then(() => element.innerHTML = 'Delete successful');
```

```js
async delete() => {
    // DELETE request using axios with async/await
    const element = document.querySelector('#delete-request-async-await .status');
    await axios.delete('https://reqres.in/api/posts/1');
    element.innerHTML = 'Delete successful';
}
```



## alias axios

Alias de métodos de petición
Por conveniencia los alias han sido proveídos para todos los métodos de petición.

axios.request(config)
axios.get(url[, config])
axios.delete(url[, config])
axios.head(url[, config])
axios.options(url[, config])
axios.post(url[, data[, config]])
axios.put(url[, data[, config]])
axios.patch(url[, data[, config]])

>[!note] NOTA
Al usar los alias, las propiedades url, method, y data no necesitan ser especificadas en la configuración.


>[!note] Probar axios
>Para probar el fetch puedes usar el sitio: `http://mock.codes/` que devuelve el error que indicas, por ejemplo: `http://mock.codes/500` te responde con error HTTP 500.


## respuesta en axios

```js
axios.get('/user/12345')
  .then(function (response) {
    console.log(response.data); //{}
    console.log(response.status); //200
    console.log(response.statusText); //text
    console.log(response.headers); //{}
    console.log(response.config); //{}
  });


```

## Configuración de petición

```js
{
  // `url` es la URL del servidor que sera usada para la petición
  url: '/user',

  // `method` es el método a ser utilizado al hacer la petición 
  method: 'get', // defecto

  // `baseURL` será precedido a `url` a no ser que `url` sea absoluto.
  // Es conveniente establecer un `baseURL` en una instancia de axios para pasar URLs relativas
  // a los métodos de esta
  baseURL: 'https://some-domain.com/api',

  // `transformRequest` permite cambios al data de la petición antes de ser enviado al servidor
  // Esto es solo aplicable para los métodos de petición 'PUT', 'POST', 'PATCH' y 'DELETE'
  // La última función en el arreglo debe regresar un string o una instancia de Buffer, ArrayBuffer,
  // FormData o Stream
  // Debes modificar el objeto headers.
  transformRequest: [function (data, headers) {
    // Haz lo que quieras para transformar data

    return data;
  }],

  // `transformResponse` permite que se realicen cambios en los datos de respuesta antes
  //  que pasen a then/catch
  transformResponse: [function (data) {
    // Haz lo que quieras para transformar data

    return data;
  }],

  // `headers` son las cabeceras personalizadas a ser enviadas
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` son los parámetros de la URL a ser enviados con la petición
  // Deben ser un objeto plano o un objeto URLSearchParams
  // NOTA: parámetros que son null o undefined no son renderizados en la URL.
  params: {
    ID: 12345
  },

  // `data` es el data a ser enviado como el cuerpo de la petición
  // Solo aplicable a los métodos de petición 'PUT', 'POST', 'DELETE , y 'PATCH'
  // Cuando no se establece `transformRequest`, debe ser uno de los siguientes tipos:
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - Solo Navegador: FormData, File, Blob
  // - Solo en Node: Stream, Buffer
  data: {
    firstName: 'Fred'
  },
  
  // sintaxis alternativa para enviar data al cuerpo
  // del método post
  // solo el valor es enviando, no la llave
  data: 'Country=Brasil&City=Belo Horizonte',

  // `withCredentials` indica cuando o no se pueden hacer peticiones cross-site Access-Control 
  // usando credenciales
  withCredentials: false, // defecto

  // `adapter` permite la manipulación personalizada de peticiones, haciendo las pruebas más fácil.
  // Retorna una promesa y provee una respuesta valida (ver lib/adapters/README.md).
  adapter: function (config) {
    /* ... */
  },

  // `auth` indica que HTTP Basic auth debe ser usado, y proveer credenciales.
  // Esto establecerá una cabecera `Authorization`, sobrescribiendo cualquier cabecera personalizada
  // existente `Authorization`, previamente a través de `headers`.
  // Ten encuenta que solo HTTP Basic auth es configurable a través de este parámetro.
  // Para tokens Bearer y otros, usa la cabecera personalizada `Authorization` en su lugar.
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

  // `responseType` indica el tipo de data con el que el servidor responderá
  // las opciones son: 'arraybuffer', 'document', 'json', 'text', 'stream'
  // solo en el navegador: 'blob'
  responseType: 'json', // defecto
  
  // `responseEncoding` indica la codificación a usar para decodificar las respuestas (solo en Node.js)
  // Nota: Ignorado para `responseType` de 'stream' o peticiones del lado del cliente
  responseEncoding: 'utf8', // defecto

  // `onUploadProgress` permite la manipulación del evento progress para subidas
  // solo en el navegador
  onUploadProgress: function (progressEvent) {
    // Haz lo que quieras con el evento nativo progress
  },

  // `onDownloadProgress` permite la manipulación del evento progress para descargars
  // solo en el navegador
  onDownloadProgress: function (progressEvent) {
    // Haz lo que quieras con el evento nativo progress
  },

  // `maxContentLength` define el tamaño máximo del contenido de la respuesta http en bytes permitidos en node.js
  maxContentLength: 2000,

  // `maxBodyLength` (opcion solo para Node) define el tamaño máximo permitido del contenido de la petición http en bytes
  maxBodyLength: 2000,

  // `validateStatus` define si resolver o rechazar la promesa para un dado
  // codigo de respuesta HTTP. Si `validateStatus` retorna `true` (o si se establece a `null`
  // o `undefined`), la promesa será resuelta; de otra manera, la promesa será
  // rechazada.
  validateStatus: function (status) {
    return status >= 200 && status < 300; // defecto
  },

  // `maxRedirects` define el número máximo de redirecciones a seguir en node.js.
  // Si se establece en 0, no habra redirecciones.
  maxRedirects: 5, // defecto

  // `socketPath` define un Socket UNIX a ser utilizado en node.js.
  // e.g. '/var/run/docker.sock' para enviar peticiones al demonio de docker (docker daemon).
  // Solo `socketPath` o `proxy` puede ser especificado.
  // Si ambos son especificados, `socketPath` es utilizado.
  socketPath: null, // defecto

  // `httpAgent` y `httpsAgent` definen un agente personalizado a ser usado al realizar una petición
  // http y https, respectivamente, en node.js. Esto permite añadir opciones como
  // `keepAlive` que no estan habilitadas por defecto.
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // `proxy` define hostname, puerto, y protocolo del servidor proxy.
  // También puedes definir tu proxy usando las variables de entorno convencionales 
  // `http_proxy` y `https_proxy`. Si estas usando variables de entorno
  // para tu configuración proxy, también puedes definir una variable de entorno `no_proxy`
  // como una lista separada por comas de dominios que no deben ser tomados en cuenta (proxied).
  // Usa `false` para desabilitar los proxies, ignorando las variables de entorno.
  // `auth` indica que HTTP Basic auth debe ser usado para conectar al proxy, y
  // proveer credenciales.
  // Esto establecerá una cabecera `Proxy-Authorization`, sobrescribiendo cualquier cabecera personalizada
  // existente `Proxy-Authorization` establecidas por `headers`.
  // Si el servidor proxy usa HTTPS, entonces debes establecer el protocolo a `https`. 
  proxy: {
    protocol: 'https',
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // `cancelToken` especifica un token de cancelación que puede ser usado para cancelar una petición
  // (ver sección sobre Cancelacion para mayor detalles)
  cancelToken: new CancelToken(function (cancel) {
  }),

  // `decompress` indica sí o no el cuerpo de la respuesta debe ser descomprimido 
  // automáticamente. Si se establece en `true` también removerá la cabecera 'content-encoding'  
  // de los objetos de respuesta de todas las respuestas descomprimidas
  // - solo en Node (XHR no puede apagar la descompresión)
  decompress: true // defecto

}

```
## Ejemplo axios.post con config

Este ejemplo cifra el payload JSON completo y envía el resultado bajo una nueva clave llamada `"SecretStuff"`:


```js
const axios = require('axios');

// 1. Crear una instancia de Axios con transformRequest configurado
const instance = axios.create({
  baseURL: 'https://api.ejemplo.com',
  transformRequest: [
    function (data, headers) {
      // Convertir el objeto de datos a una cadena JSON y cifrarla
      const encryptedString = encryptPayload(JSON.stringify(data));
      
      // Crear un nuevo objeto con la estructura que espera el servidor
      const transformedData = {
        SecretStuff: encryptedString
      };

      // Convertir el objeto a JSON string antes de enviarlo
      return JSON.stringify(transformedData);
    }
  ],
  headers: {
    'Content-Type': 'application/json; charset=utf-8'
  }
});

// 2. Función de ejemplo para "cifrar" los datos (simulada)
function encryptPayload(payload) {
  // En un caso real, aquí iría tu lógica de cifrado real
  return btoa(payload); // Simulación usando base64
}

// 3. Realizar la solicitud POST
const postData = {
    id: 1,
    nombre: 'Juan'
};

instance.post('/endpoint', postData)
  .then(response => {
    console.log('Éxito:', response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

## Ejemplo de axios.get con config

ejemplo práctico de cómo usar `axios.get` con `transformResponse` para modificar los datos de respuesta antes de que sean procesados por tu aplicación:

```js
axios.get('https://api.ejemplo.com/datos', {
  transformResponse: [
    // transformResponse recibe los datos en formato string
    function (data) {
      // Primero, convertimos el string JSON a un objeto JavaScript
      const parsedData = JSON.parse(data);
      
      // Ahora podemos modificar los datos como necesitemos
      // Ejemplo: agregar un nuevo campo calculado
      parsedData.timestampProcesamiento = new Date().toISOString();
      
      // Ejemplo: transformar nombres de campos (snake_case a camelCase)
      if (parsedData.user_name) {
        parsedData.userName = parsedData.user_name;
        delete parsedData.user_name;
      }
      
      // La función debe devolver los datos transformados
      return parsedData;
    }
  ]
})
.then(response => {
  // response.data ya contiene los datos transformados
  console.log('Datos transformados:', response.data);
  console.log('Nombre de usuario:', response.data.userName);
  console.log('Timestamp:', response.data.timestampProcesamiento);
})
.catch(error => {
  console.error('Error:', error);
});
```

## Referencias

* [Axios documentación en español](https://axios-http.com/es/docs/req_config)
