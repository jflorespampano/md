# usar express

Biblioteca para manejo de peticions http

## Cargar express en su proyecto
```sh
#iniciar proyecto con los valores de default
npm init -y
#cargar express
npm i express
#cargar dotenv
npm i dotenv
```

Crear archivo: .env
```js
PORT=3000
```
agregar la entrada: "type":"module", al package.json

## middleware

Las funciones de middleware son una parte crucial de una aplicación Express.js, ya que le permiten realizar varias tareas, como:

1. Manipulación de solicitudes y respuestas: modifique los objetos de solicitud y respuesta antes de que lleguen a los controladores de ruta.
2. Manejo de errores: detecte y maneje los errores antes de que se propaguen a los controladores de ruta.
3. Autenticación y autorización: verifique las credenciales y los permisos de los usuarios antes de permitir el acceso a las rutas.
4. Almacenamiento en caché: implemente mecanismos de almacenamiento en caché para optimizar el rendimiento.
5. Registro: registre solicitudes y respuestas para fines de auditoría y depuración.

Estructura básica de middleware

Una función de middleware toma tres argumentos:

1. req (objeto de solicitud): contiene información sobre la solicitud entrante.
2. res (objeto de respuesta): le permite enviar una respuesta al cliente.
3. next (función): llama a la siguiente función de middleware en la cadena o finaliza el ciclo de solicitud-respuesta.

Ejemplo
```js
const myMiddleware = (req, res, next) => {
  // Perform some operation on the request or response
  console.log(`Received request: ${req.method} ${req.url}`);
  next(); // Call the next middleware function
};
```
Funciones middleware de biblioteca: json() y text(), son usadas para la recepcion de datos de diferetes formatos en express
con ellas podemos recibir datos del body (con formato texto  o json) para post, put.

express.json() es una función de middleware integrada en Express.js, introducida en la versión 4.16.0. Analiza las solicitudes entrantes con cargas útiles JSON y se basa en el módulo body-parser. Este middleware está habilitado de forma predeterminada al crear una nueva aplicación Express.

express.text() es una función de middleware integrada en Express.js, un popular framework web de Node.js. Analiza las cargas útiles de las solicitudes entrantes en una cadena y se basa en el middleware body-parser

El middleware urlencoded() de Express.js se utiliza para analizar solicitudes entrantes con cargas útiles codificadas en URL. Es una función de middleware integrada que analiza el cuerpo de la solicitud como datos codificados en URL y completa el objeto req.body con los datos analizados. La opción **extended** permite la inclusión de objetos anidados en los datos analizados. Si se establece en falso, solo se analizarán pares clave-valor planos. El middleware urlencoded solo analiza las solicitudes con el encabezado Content-Type establecido en application/x-www-form-urlencoded. Si el encabezado no está presente o está establecido en un valor diferente, el middleware no analizará el cuerpo de la solicitud.
En Express.js 4.16.0 y versiones posteriores, el middleware body-parser ya no es necesario y se puede utilizar en su lugar el middleware urlencoded integrado.

```js
import express from "express"
import dotenv from 'dotenv'

dotenv.config() //cargar las variables de entorno del archivo .env en process.env
const PORT=process.env.PORT //cargar el numeo de puerto

const app=express()
//middleware para  aceptar json y texto
app.use(express.json())
app.use(express.text())
app.use(express.urlencoded({extended:false}));
app.get("/",(req,res)=>{
    res.set({"content-type":"text/html; charset=utf-8"})
    res.end(
        `
        <h1>Hola mundo</h1>
        `
    )
})
//parametros en la url
//espera una url asi: http://localhost:3000/user/779-jflores-59
app.get("/user/:id-:name-:edad",(req,res)=>{
    res.set({"content-type":"text/html; charset=utf-8"})
    //params almacena los  parametros enviados por la url
    console.log(req.params)
    res.end(
        `
        <h1>${req.params.name} binevenidos a express id=${req.params.id}</h1>
        `
    )
})
//parametros query
//espera:http://localhost:3000/search?id=779&nombre=alejandro flores&edad=59
app.get('/search',(req,res)=>{
    const data=req.query
    console.log(data)
    res.send(
        `
        <h1>${data.id} bienvenido ${data.nombre} tu edad ${data.edad}</h1>
        `
    )
})
//parametros en el body
//espera:http://localhost:3000/account, con un body en formato json o Form-encode
app.post('/account',(req,res)=>{
    console.log(req.body)
    res.send(
        `
        <h2>Hola recibiendo POST ${req.body.nombre} edad ${req.body.edad}</h2>
        `
        )
})
app.put('/account',(req,res)=>{
    console.log(req.body)
    res.send(
        `
        <h2>Hola recibiendo PUT ${req.body.nombre} edad ${req.body.edad}</h2>
        `
        )
})
app.patch('/account',(req,res)=>{
    console.log(req.body)
    res.send(
        `
        <h2>Hola recibiendo PATCH ${req.body.nombre} edad ${req.body.edad}</h2>
        `
        )
})

//espera id comom parametro query: http://localhost:3000/search?id=779
app.delete('/account',(req,res)=>{
    console.log(req.query)
    res.send(
        `
        <h2>Hola recibiendo con DELETE un id=${req.query.id}</h2>
        `
        )
})

app.listen(PORT,()=>{
    console.log(`iniciando express desde: http://localhost:${PORT}/`)
})
```

## manejo de rutas de directorio path

```js
process.cwd() //devuelve el directorio de trabajo corriente del proceso de Node.js
```