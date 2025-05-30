## curl

Una URL (Uniform Resource Locator) es una direccion que es dada a un recurso único en la Web. En teoria, cada URL válida apunta a un único recurso.

Curl significa cliente URL y es una herramienta de línea de comandos gratuita para transferir archivos con sintaxis de URL. Curl admite varios protocolos, incluidos certificados HTTP, FTP, SMB y SSL. Hay varios clientes Curl para Windows, Linux, macOS, Android e iOS, y ahora con el cliente ReqBin Online para la web. Los desarrolladores pueden utilizar la biblioteca libcurl para integrar Curl en sus aplicaciones C/C++, Java, PHP y Python. Curl se ha convertido en la herramienta principal para describir llamadas API en la documentación debido a su popularidad y facilidad de uso.

Formato general:
```sh
curl -X POST/GET/PATCH/DELETE [url]
-H "Content-Type: [content  type]"
-d '[request data]'
-v/-i
```
Las opciones y sus sinonimos:

-X sinonimo --request
-H sinonimo --header
-d sinonimo --data
La opción -v no muestra las cabeceras, la enviada por el cliente y la que devuelve el servidor.
La opción -i nos da la información resumida
La opcion -I devuelve solo los encabezados de la petición

La opcion -H indica el tipo de codificación de datos. 
Codificaciones en http
```sh
Content-Type: application/json
Content-Type: application/x-www-form-urlencoded
Content-Type: text/html; charset=utf-8
Content-Type: multipart/form-data; boundary=something
```

## Actividad: usando Get

En una ventana bash pruebe las sentencias:
```sh
curl -X GET https://jsonplaceholder.typicode.com/posts
#por default si no se pone -X GET se asume que es un get por tato lo anterio es igual que:
curl https://jsonplaceholder.typicode.com/posts
```

## enviar parametros en la url

```sh
#enviar parametros en la url:
#en curl, se debe poner \ para escapar el & en la consola de linux
curl http://localhost:3000/?id=23\&nombre=juan perez\&correo=juan@mail\&edad=23
```

## Post enviando codificación en urlencoded

Cuando pasa parametros en curl con -d x deafult se usa la codificación: 
'Content-Type: application/x-www-form-urlencoded' 
de no usar esa se debe especificar otra con -H

```sh
curl -X POST  http://localhost:3000/user -d 'id=23&nombre=ana perez&correo=ana@mail&edad=32'
curl --request POST https://jsonplaceholder.typicode.com/posts -d 'title=23&body=cuerop del body&userId=32'
```

## Post enviando codificación json
```sh
curl   -X POST http://localhost:3000/user -H "Content-Type: Application/json" -d '{"id":"23","nombre":"ana perez","correo":"ana@mail","edad":32}'
curl -X POST https://jsonplaceholder.typicode.com/posts -H "Content-Type: Application/json" -d '{"title":"23","body":"cuerop de...","userId":32}'
```
o usando
```sh
curl --request POST https://jsonplaceholder.typicode.com/posts -d 'title=23&body=cuerop del body&userId=32'
curl --request POST https://jsonplaceholder.typicode.com/posts -H "Content-Type: Application/json" -d '{"title":"23","body":"cuerop de...","userId":32}'
```


En linux puedo enviar la sentencia en varias lineas dividiendo con \
```sh
curl --request POST https://jsonplaceholder.typicode.com/posts \
-H "Content-Type: Application/json" \
-d '{"title":"23","body":"cuerop de...","userId":32}'
```

En windows usando cmd las lineas se dividen usondo ^, y escapar comillas
```sh
curl --request POST https://jsonplaceholder.typicode.com/posts ^
-H "Content-Type: Application/json" ^
-d "{\"title\":\"23\",\"body\":\"cuerpo de...\",\"userId\":32}"
```
En windows usando power shell no se recomienda por que usa su propio curl (invoke-restmethod)

# Ejemplo con https://jsonplaceholder.typicode.com/posts


## Ejemplo con Get

Las 3 sentencias siguientes son equivalentes
```sh
curl https://jsonplaceholder.typicode.com/posts
curl --request GET https://jsonplaceholder.typicode.com/posts
curl -X GET https://jsonplaceholder.typicode.com/posts
```

## Ejemplo con Post enviando urlencode

```sh
curl -X POST https://jsonplaceholder.typicode.com/posts -d 'title=23&body=cuerop del body&userId=32'
curl --request POST https://jsonplaceholder.typicode.com/posts -d 'title=23&body=cuerop del body&userId=32'
```

## Ejemplo enviando json

```sh
curl --header "Content-Type: Application/json" https://jsonplaceholder.typicode.com/posts -d '{"title":"23","body":"cuerop de...","userId":32}' 

curl -X POST -H "Content-Type: Application/json" https://jsonplaceholder.typicode.com/posts -d '{"title":"23","body":"cuerop de...","userId":32}'

curl -X PATCH http://localhost:3000/user -H "content-type: application/json" -d '{"id":34,"nombre":"luis","correo":"micorreo","edad":34}'
```
## Archivos

enviar solicitud y almacenar respuesta en un archivo
```sh
curl -o datos.txt ...
```
Enviar datos json desde un archivo
```sh
curl -d "@data.json" ...
```

## post con datos en un archivo

Archivo data.json
```json
{"title":"hola mundo","body":"mi primer post"}
```
Ejemplos:
```sh
curl -X POST -H "Content-Type: Application/json"  -d "@data.json"  https://jsonplaceholder.typicode.com/posts
```

## ejemplos

Ejemplo usàndo datafake
```sh
#solicitar datos get
curl  https://jsonplaceholder.typicode.com/posts
curl -o respuesta.txt https://jsonplaceholder.typicode.com/posts
#enviar datos url-encode con get
curl -d 'title=hola mundo&body=mi primer post'  https://jsonplaceholder.typicode.com/posts
#enviar datos json con get 
curl -H "Content-Type: Application/json"  -d '{"title":"hola mundo","body":"mi primer post"}'  https://jsonplaceholder.typicode.com/posts
#enviar datos json con post
curl -X POST -H "Content-Type: Application/json"  -d '{"title":"hola mundo","body":"mi primer post"}'  https://jsonplaceholder.typicode.com/posts
#enviar datos url-encode post forma 1
curl -X POST -H "Content-Type: application/x-www-form-urlencoded"  -d 'title=hola mundo&body=mi primer post'  https://jsonplaceholder.typicode.com/posts
#enviar datos url-encode post forma 2
curl -X POST -d 'title=hola mundo&body=mi primer post'  https://jsonplaceholder.typicode.com/posts
#enviar datos url-encode post forma 3
curl -X POST -d 'title=hola mundo' -d 'body=mi primer post'  https://jsonplaceholder.typicode.com/posts
#enviar a un sitio local
curl -i -d '{"id":56,"nombre":"juan","carrera":"isc"}' -H "Content-Type: Application/json" http://localhost/proyectos/alumnosArray/recibeJson.php
```

## autenticación

```sh
curl -H "Authorization: Bearer MI_TOKEN_SECRETO_DE:AUTENTICACION" https://...
#cargando el token desde una variable de entorno
curl -H "Authorization: Bearer $ACCES_TOKEN" https://...
#cargarlod ede un archivo .env
source .env &&
curl -H "Authorization: Bearer $ACCES_TOKEN" https://...
#si se requiere usuario y contraseña en lugar de un token
curl -u usuario:contraseña https://...
#o cargando desde un archivo .env
(
    source .env &&
    curl -u $USER:$PASSWORD https://...
)

```
## descrgar archivos con curl
```sh
curl -o ~/downloads/archivo.zip https://example.com/archivo.zip
```

## referencias

[referencia a curl](https://reqbin.com/req/c-bjcj04uw/curl-send-cookies-example)