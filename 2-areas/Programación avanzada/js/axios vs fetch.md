
La siguiente tabla compara sus características clave para ayudarte a visualizar las diferencias:

| Característica        | Axios                                                                     | Fetch                                                                                           |
| --------------------- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Instalación**       | Librería externa que requiere instalación                                 | API nativa del navegador, no necesita instalación                                               |
| **Manejo de JSON**    | Conversión automática de datos a JSON                                     | Necesita llamar a `.json()` de forma manual y asíncrona                                         |
| **Manejo de errores** | Rechaza promesas automáticamente con códigos de error HTTP (ej. 404, 500) | Solo rechaza por fallos de red; requiere verificación manual de `response.ok` para errores HTTP |
| **Timeouts**          | Configuración simple con propiedad `timeout`                              | Requiere el uso de `AbortController` y `AbortSignal`                                            |
| **Interceptores**     | Sí, para modificar peticiones/respuestas globalmente                      | No, requiere implementación manual                                                              |
| **Compatibilidad**    | Amplia compatibilidad con navegadores antiguos usando `XMLHttpRequest`    | Solo navegadores modernos; requiere _polyfill_ para versiones antiguas                          |
| **Envío de datos**    | Usa propiedad `data`; envía objetos JS directamente                       | Usa propiedad `body`; debe convertir datos con `JSON.stringify()`                               |

- **Elige Fetch** si priorizas una solución nativa y ligera, sin dependencias externas, y no te importa escribir un poco más de código para funcionalidades avanzadas. Es ideal para proyectos simples o cuando se quiere evitar agregar librerías.
- **Elige Axios** si necesitas características avanzadas como interceptores, cancelación de peticiones, manejo de errores más robusto o un código más limpio y conciso. Es perfecto para aplicaciones grandes y complejas donde la productividad del desarrollador y la consistencia del código son importantes.

## interceptores

En este ejemplo, el interceptor agrega automáticamente un encabezado de autorización con un token a todas las solicitudes salientes.
```js
const axios = require('axios');

// Interceptor de solicitudes
axios.interceptors.request.use(config => {
  // Modificar la solicitud antes de enviarla
  const token = 'mi-token-de-autenticacion';
  if (token) {
    config.headers['Authorization'] = `Bearer ${token}`;
  }
  return config;
}, error => {
  // Manejar el error de la solicitud
  return Promise.reject(error);
});

// Realizar una solicitud GET
axios.get('https://api.ejemplo.com/datos')
  .then(response => {
    console.log('Datos recibidos:', response.data);
  })
  .catch(error => {
    console.error('Error en la solicitud:', error);
  });
```

## interceptores de respuesta

En este caso, el interceptor maneja errores HTTP de manera global, mostrando un mensaje específico si la solicitud falla por errores 401 (no autorizado) o 500 (error interno del servidor).

```js
axios.interceptors.response.use(response => {
  // Modificar la respuesta antes de devolverla
  return response;
}, error => {
  // Manejar errores de la respuesta
  if (error.response && error.response.status === 401) {
    console.log('No autorizado. Redirigiendo al login...');
    // Aquí podrías redirigir al login, por ejemplo.
  } else if (error.response && error.response.status === 500) {
    console.log('Error interno del servidor.');
  }
  return Promise.reject(error);
});

// Realizar una solicitud GET
axios.get('https://api.ejemplo.com/datos')
  .then(response => {
    console.log('Datos recibidos:', response.data);
  })
  .catch(error => {
    console.error('Error en la solicitud:', error);
  });
```


## Ejemplo de manejo de errores con interceptor

**Crear una Instancia de Axios**: Configuración base para tu API

```js
// axiosInstance.js
import axios from 'axios';

const axiosInstance = axios.create({
  baseURL: 'https://api.ejemplo.com', // Tu URL base
  timeout: 10000, // Timeout opcional
});
```
**Agregar un Interceptor de Solicitud**: Se ejecuta antes de que cada petición salga. Se usa comúnmente para añadir tokens de autenticación

```js
axiosInstance.interceptors.request.use(
  (config) => {
    // Obtener el token de donde lo almacenes (ej. localStorage)
    const token = localStorage.getItem('authToken');
    if (token) {
      // Inyectar el token en los headers de la petición
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config; // Es crucial devolver la configuración
  },
  (error) => {
    // Manejar el error de la petición
    return Promise.reject(error);
  }
);
```

**Agregar un Interceptor de Respuesta**: Se ejecuta cuando se recibe una respuesta. Es ideal para manejar errores globalmente
```js
axiosInstance.interceptors.response.use(
  (response) => {
    // Cualquier código de estado 2xx hace que se ejecute esto
    return response; // Devuelve la respuesta sin modificar
  },
  (error) => {
    // Cualquier código de estado fuera de 2xx hace que se ejecute esto
    if (error.response) {
      switch (error.response.status) {
        case 401:
          console.error("No autorizado - Redirigiendo al login...");
          // Redirigir al usuario a la página de login
          break;
        case 403:
          console.error("Prohibido - No tienes permisos.");
          break;
        case 404:
          console.error("Recurso no encontrado.");
          break;
        case 500:
          console.error("Error interno del servidor.");
          break;
      }
    }
    return Promise.reject(error); // Rechaza la promesa para manejo posterior
  }
);

export default axiosInstance; // Exporta tu instancia personalizada
```

**Usar la Instancia en tu Aplicación**: Importa y usa la instancia personalizada en tus componentes en lugar de `axios` global
```js
// En tu componente React, Vue, etc.
import axiosInstance from './axiosInstance';

const fetchData = async () => {
  try {
    const response = await axiosInstance.get('/products');
    console.log(response.data);
  } catch (error) {
    // Los errores ya fueron manejados por el interceptor, pero puedes hacer un manejo específico aquí también.
    console.error('Error capturado en el componente:', error);
  }
};
```
