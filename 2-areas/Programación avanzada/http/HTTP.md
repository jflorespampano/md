
HTTP es el **protocolo fundamental** de la web que permite la comunicación entre clientes (navegadores) y servidores. Es la base sobre la que se construye internet.

### Definición básica:

- **Protocolo de aplicación** para transferir hipertexto
- **Modelo cliente-servidor** sin estado (stateless) 
- **Solicitud-respuesta** entre navegador y servidor
- **Puerto por defecto**: 80

Flujo básico

```text
Cliente (Navegador) → Solicitud HTTP → Servidor Web
Cliente (Navegador) ← Respuesta HTTP ← Servidor Web
```

![[Excalidraw/http.excalidraw.md#^area=t3nRO0KYuG4yVhhYiAZro]]
## **Métodos HTTP Principales (Verbos)**

| Método     | Descripción           | Idempotente | Seguro |
| ---------- | --------------------- | ----------- | ------ |
| **GET**    | Obtener recursos      | ✅ Sí        | ✅ Sí   |
| **POST**   | Enviar datos          | ❌ No        | ❌ No   |
| **PUT**    | Actualizar/reemplazar | ✅ Sí        | ❌ No   |
| **DELETE** | Eliminar recursos     | ✅ Sí        | ❌ No   |
| **PATCH**  | Modificación parcial  | ❌ No        | ❌ No   |
| **HEAD**   | Solo headers          | ✅ Sí        | ✅ Sí   |

La **idempotencia** es una propiedad importante en HTTP que indica que una misma solicitud hecha múltiples veces tendrá el mismo efecto que si se hiciera una sola vez.

Tabla de idempotencia

| Verbo HTTP | Idempotente | Explicación                                                                                              |
| ---------- | ----------- | -------------------------------------------------------------------------------------------------------- |
| **GET**    | ✅ Sí        | Obtener un recurso no cambia el estado.                                                                  |
| **PUT**    | ✅ Sí        | Actualizar un recurso con el mismo dato múltiples veces no cambia el resultado.                          |
| **DELETE** | ✅ Sí        | Eliminar un recurso una vez o múltiples veces deja el recurso eliminado.                                 |
| **POST**   | ❌ No        | Cada solicitud puede crear un nuevo recurso, por lo que múltiples solicitudes tendrán múltiples efectos. |
| **PATCH**  | ❌ No        | Una actualización parcial puede no ser idempotente (depende de cómo se implemente).                      |
## **Códigos de Estado HTTP**

### Categorías principales:

|Código|Categoría|Significado|
|---|---|---|
|**1xx**|Informativo|Petición recibida, proceso continuo|
|**2xx**|Éxito|Petición completada satisfactoriamente|
|**3xx**|Redirección|Acción adicional necesaria|
|**4xx**|Error del cliente|Petición mal formada|
|**5xx**|Error del servidor|Servidor falló al completar|
Códigos mas comunes

```text
200 OK - Todo bien
201 Created - Recurso creado
400 Bad Request - Petición mal formada
401 Unauthorized - No autenticado
403 Forbidden - No autorizado
404 Not Found - Recurso no existe
500 Internal Server Error - Error del servidor
```

Estructura de una petición

```http
GET /index.html HTTP/1.1
Host: www.ejemplo.com
User-Agent: Mozilla/5.0
Accept: text/html
Accept-Language: es-ES
Connection: keep-alive
```
### Partes de la petición:

1. **Línea de solicitud**: `Método URI Versión-HTTP`
2. **Headers**: Metadatos de la petición
3. **Body** (opcional): Datos enviados (en POST, PUT)

## **Estructura de una Respuesta HTTP**

### Response (Servidor → Cliente):

```http
HTTP/1.1 200 OK
Date: Mon, 23 May 2023 22:38:34 GMT
Content-Type: text/html; charset=UTF-8
Content-Length: 138
Last-Modified: Wed, 08 Jan 2023 23:11:55 GMT
Server: Apache/2.4.1

<!DOCTYPE html>
<html>
<head>
    <title>Ejemplo</title>
</head>
<body>
    <h1>Hola Mundo</h1>
</body>
</html>
```

### Partes de la respuesta:

1. **Línea de estado**: `Versión-HTTP Código Mensaje`
2. **Headers**: Metadatos de la respuesta
3. **Body**: Contenido solicitado

## **Headers HTTP Importantes**

### Headers comunes:

| Header            | Descripción                                                                           | Ejemplo                                                                                                                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Content-Type**  | Tipo de contenido                                                                     | `application/json`                                                                                                                                                                      |
| **Authorization** | Credenciales                                                                          | `Bearer token123`                                                                                                                                                                       |
| **User-Agent**    | Información del cliente                                                               | `Mozilla/5.0...`                                                                                                                                                                        |
| **Cache-Control** | Control de caché                                                                      | `max-age=3600`                                                                                                                                                                          |
| **Cookie**        | Cookies del sitio                                                                     | `session=abc123`                                                                                                                                                                        |
| Accept-Language   | idiomas que prefiere el usuario para la respuesta                                     | es-ES                                                                                                                                                                                   |
| Connection        | controla si la conexión de red permanece abierta después de que la transacción actual | keep-alive (la conexión debe mantenerse abierta (en HTTP/1.0, por defecto se cierra). En HTTP/1.1, las conexiones son persistentes por defecto, por lo que este valor no es necesario,) |
| Authorization     | contiene las credenciales para autenticar a un cliente                                | Authorization: <tipo> <credenciales>                                                                                                                                                    |


### Esquemas de autenticación comunes

|Esquema|Descripción|Ejemplo|
|---|---|---|
|**Basic**|Credenciales en base64 (usuario:contraseña)|`Authorization: Basic dXNlcjpwYXNz`|
|**Bearer**|Token de acceso (OAuth, JWT)|`Authorization: Bearer eyJ0eXAi...`|
|**Digest**|Autenticación con hash (más segura que Basic)|`Authorization: Digest username="...", ...`|
|**API Key**|A veces se usa un esquema personalizado|`Authorization: Apikey 12345abc`|
## Versiones de http

|Versión|Año|Características principales|
|---|---|---|
|**HTTP/0.9**|1991|Solo GET, texto plano|
|**HTTP/1.0**|1996|Headers, métodos, códigos de estado|
|**HTTP/1.1**|1997|Conexiones persistentes, chunked encoding|
|**HTTP/2**|2015|Multiplexación, compresión headers|
|**HTTP/3**|2022|QUIC sobre UDP, menor latencia|

## **HTTPS - HTTP Seguro**

### Diferencias clave:

- **HTTP**: Texto plano (inseguro)
- **HTTPS**: Cifrado con SSL/TLS (seguro)
- **Puerto**: 443 en lugar de 80
- **Autenticación** del servidor

Ventajas https

```http
✅ Confidencialidad - Datos cifrados
✅ Integridad - Datos no modificados
✅ Autenticación - Servidor verificado
```

## Ejemplo en js

```js
// GET request
fetch('https://api.ejemplo.com/usuarios')
  .then(response => {
    if (!response.ok) throw new Error('Error HTTP: ' + response.status);
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

// POST request
fetch('https://api.ejemplo.com/usuarios', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer ' + token
  },
  body: JSON.stringify({
    nombre: 'Ana',
    email: 'ana@ejemplo.com'
  })
});
```
## ¿Qué sigue?

[[Errores http]]
