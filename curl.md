## curl

Una URL (Uniform Resource Locator) no es más que una direccion que es dada a un recurso único en la Web. En teoria, cada URL válida apunta a un único recurso.

Curl significa cliente URL y es una herramienta de línea de comandos gratuita para transferir archivos con sintaxis de URL. Curl admite varios protocolos, incluidos certificados HTTP, FTP, SMB y SSL. Hay varios clientes Curl para Windows, Linux, macOS, Android e iOS, y ahora con el cliente ReqBin Online para la web. Los desarrolladores pueden utilizar la biblioteca libcurl para integrar Curl en sus aplicaciones C/C++, Java, PHP y Python. Curl se ha convertido en la herramienta principal para describir llamadas API en la documentación debido a su popularidad y facilidad de uso.

Formato general:
```sh
curl -X POST/GET/PATCH/DELETE [url]
-H "Content-Type: [content  type]"
-d '[request data]'
-v/-i
```
La opción -v no muestra las cabeceras, la enviada por el cliente y la que devuelve el servidor.
La opción -i nos da la información resumida

Las opciones y sus sinonimos:
-X sinonimo --request
-H sinonimo --header
-d sinonimo --data

## resumen encode

Codificaciones en http
```sh
Content-Type: text/html; charset=utf-8
Content-Type: application/json
Content-Type: application/x-www-form-urlencoded
Content-Type: multipart/form-data; boundary=something
```
## usando Get
```sh
curl -X GET https://jsonplaceholder.typicode.com/posts
#por default si no se pone -X GET se asume que es un get
#ejemlos
curl https://jsonplaceholder.typicode.com/posts
#tambin se pueden enviar parametros en la url
#en curl, se debe poner \ para escapar el & en la consola de linux
curl http://localhost:3000/?id=23\&nombre=juan perez\&correo=juan@mail\&edad=23
curl http://localhost:3000/
curl http://localhost:3000/user/ana pacheco
```

## Post enviando urlencoded

Cuando pasa parametros en curl con -d x deafult se usa la codificación: 
'Content-Type: application/x-www-form-urlencoded' 
de no usar esa se debe especificar otra con -H

```sh
curl -X POST  http://localhost:3000/user -d 'id=23&nombre=ana perez&correo=ana@mail&edad=32'
```

## Post enviando json
```sh
curl   -X POST http://localhost:3000/user -H "Content-Type: Application/json" -d '{"id":"23","nombre":"ana perez","correo":"ana@mail","edad":32}'
```
o usando
```sh
curl --header "Content-Type: Application/json" -d '{"id":"23","nombre":"ana perez","correo":"ana@mail","edad":32}' http://localhost:3000/user
```

# Ejemplo con https://jsonplaceholder.typicode.com/posts
## Ejemplo con Get

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

## Ejemplo con Post enviando json

```sh
curl --header "Content-Type: Application/json" https://jsonplaceholder.typicode.com/posts -d '{"title":"23","body":"cuerop de...","userId":32}' 

curl -X POST -H "Content-Type: Application/json" https://jsonplaceholder.typicode.com/posts -d '{"title":"23","body":"cuerop de...","userId":32}'

curl -X PATCH http://localhost:3000/user -H "content-type: application/json" -d '{"id":34,"nombre":"luis","correo":"micorreo","edad":34}'
```
## varios

enviar solicitud y almacenar respuesta en un archivo
```sh
curl -o datos.txt ...
```
Enviar datos json desde un archivo
```sh
curl -d "@data.json" ...
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

con datos en un archivo

Archivo data.json
```json
{"title":"hola mundo","body":"mi primer post"}
```
Ejemplos:
```sh
curl -X POST -H "Content-Type: Application/json"  -d "@data.json"  https://jsonplaceholder.typicode.com/posts
```

[referencia a curl](https://reqbin.com/req/c-bjcj04uw/curl-send-cookies-example)