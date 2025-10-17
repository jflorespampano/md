

>[!note] Nota
>Funciona correctamente en NODE
>

Para pruebas rápidas y sin configuración, los servicios web que devuelven códigos de estado específicos son la opción más sencilla.

- **httpstat.us**: Simula cualquier código de estado HTTP[](https://stackoverflow.com/questions/65327570/ways-to-simulate-error-responses-on-request-in-browser). Solo necesitas hacer una petición a una URL como `https://httpstat.us/400` para probar un error 400 "Bad Request" o `https://httpstat.us/500` para un error interno del servidor[](https://stackoverflow.com/questions/65327570/ways-to-simulate-error-responses-on-request-in-browser).
    
- **Uso con `fetch`**: Integra estos servicios en tu código JavaScript usando `fetch` para probar tus manejadores de error:
- 
```js
    console.log("Hello, 'World'!");
    // Ejemplo usando fetch
    fetch('https://mock.codes/429')
    .then(response => {
        // El código de estado HTTP está en response.status
        console.log('Código de error HTTP:', response.status);
        console.log('Texto del estado:', response.statusText);
        // Puedes lanzar un error si la respuesta no es exitosa
        if (!response.ok) {
        throw new Error(`Error ${response.status}: ${response.statusText}`);
        }
        return response.json();
    })
    .then(data => {
        // Manejar los datos de una respuesta exitosa aquí
        console.log('Datos:', data);
    })
    .catch(error => {
        // Manejar cualquier error aquí (errores de red o los que lanzaste arriba)
        console.error('Error capturado:', error.message);
    });
```