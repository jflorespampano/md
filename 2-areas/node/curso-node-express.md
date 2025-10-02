# usar express

Biblioteca para manejo de peticiones http. Express es el framework web más popular de Node, y es la librería subyacente para un gran número de otros frameworks web de Node populares. Proporciona mecanismos para:

1. Escritura de manejadores de peticiones con diferentes verbos HTTP en diferentes caminos URL (rutas).
2. Integración con motores de renderización de "vistas" para generar respuestas mediante la introducción de datos en plantillas.
3. Establecer ajustes de aplicaciones web como qué puerto usar para conectar, y la localización de las plantillas que se utilizan para renderizar la respuesta.
4. Añadir procesamiento de peticiones "middleware" adicional en cualquier punto dentro de la tubería de manejo de la petición.

A pesar de que Express es en sí mismo bastante minimalista, los desarrolladores han creado paquetes de middleware compatibles para abordar casi cualquier problema de desarrollo web. Hay librerías para trabajar con cookies, sesiones, inicios de sesión de usuario, parámetros URL, datos POST, cabeceras de seguridad y muchos más. Puedes encontrar una lista de paquetes middleware mantenida por el equipo de Express en Express Middleware (junto con una lista de algunos de los paquetes más populares de terceros).

## Cargar express en su proyecto
```sh
#iniciar proyecto con los valores de default
npm init -y
#cargar express
npm i express
```

Agregar la entrada: "type":"module", al package.json, así:
```json
{
  "name": "servidor express",
  "version": "1.0.0",
  "description": "ejemplo de express",
  "main": "index.mjs",
  "type":"module"
  "scripts": {
    "dev": "node run index"
  },
  "author": "jflores",
  "license": "ISC",
  "keywords": [],
    "dependencies": {
    "express": "^4.21.0",
  }
}

```

## ejemplo básico

```js
import express from 'express';
const app = express();

app.get('/', (req, res) => {
    res.send('Hola mundo'); //el status 200 va x default
	// res.status(200).send('Hola mundo');
	// res.status(200).set({'Content-Type': 'text/html'}).send('<p>Hola mundo</p>');
    // res.status(200).json({success:true, data:"mis datos", error:null});
})
const PORT = 3000;

app.listen(PORT, () => {
	console.log(`Servidor corriendo el el PUERTO ${PORT}`);
})
```

Otras formas de devolver respuesta:

* con encabezado usando writehead:
```js
    response.writeHead(200, { "Content-Type": "text/plain" });
    // Se responde, en el cuerpo de la respuesta con el mensaje "Hello World"
    response.end("Hola Mundo!\n");
```
es (recomendado) el siguiente código mas intuitivo:
```js
// Equivalente en Express (recomendado)

  res.status(200)
     .set({
       'Content-Type': 'text/plain',
       'Custom-Header': 'Hello-World',
     })
     .send('¡Hola con métodos Express!');

```

* Con json() no se necesita JSON.stringify
```js
res.status(200).json({success:true, data:"mis datos", error:null});
```

## devolver html

```js
import express from 'express';
const app = express();

app.get('/', (req, res) => {
    const html = `
        <!DOCTYPE html>
        <html>
            <head>
                <title>Mi Página</title>
            </head>
            <body>
                <h1>¡Hola desde Express!</h1>
                <p>Este HTML se envió directamente como string.</p>
            </body>
        </html>
    `;
    res.set({
       'Content-Type': 'text/html'
     }).send(html); // Envía el HTML como respuesta
});

app.listen(3000, () => console.log('Servidor en http://localhost:3000'));
```

## servidor estatico

```js
import express from 'express'
const app = express();

app.use(express.static('public'));

app.get('/', (req, res) => {
    res.sendFile(path.join('public', 'index.html'));
});

app.listen(3000, () => console.log('Servidor corriendo en http://localhost:3000'));
```

## middleware

Las funciones de middleware son una parte crucial de una aplicación Express.js, ya que le permiten realizar varias tareas, como:

1. Manipulación de solicitudes y respuestas: modifique los objetos de solicitud y respuesta antes de que lleguen a los controladores de ruta.
2. Manejo de errores: detecte y maneje los errores antes de que se propaguen a los controladores de ruta.
3. Autenticación y autorización: verifique las credenciales y los permisos de los usuarios antes de permitir el acceso a las rutas.
4. Almacenamiento en caché: implemente mecanismos de almacenamiento en caché para optimizar el rendimiento.
5. Registro: registre solicitudes y respuestas para fines de auditoría y depuración.

El middleware en Express.js es una función que tiene acceso a todo el objeto de solicitud (req), todo el objeto de respuesta (res) y la siguiente función de middleware en el ciclo de solicitud-respuesta de la aplicación.

### Estructura básica de middleware

Una función de middleware toma tres argumentos:

1. req (objeto de solicitud): contiene información sobre la solicitud entrante.
2. res (objeto de respuesta): le permite enviar una respuesta al cliente.
3. next (función): llama a la siguiente función de middleware en la cadena o finaliza el ciclo de solicitud-respuesta.

Ejemplo
```js
const myMiddleware = (req, res, next) => {
  // realiazar alguna operación en el request o response
  console.log(`Received request: ${req.method} ${req.url}`);
  next(); // llamar al siguiente middleware 
};

//cargarla antes de las funciones de atencion a get/post/etc, se carga así:
app.use(myMiddleware)
```

Funciones middleware de biblioteca: json() y text(), son usadas para la recepcion de datos de diferetes formatos en express
con ellas podemos recibir datos del body (con formato texto  o json) para post, put.

express.json() es una función de middleware integrada en Express.js, introducida en la versión 4.16.0. Analiza las solicitudes entrantes con cargas útiles JSON y se basa en el módulo body-parser. Este middleware está habilitado de forma predeterminada al crear una nueva aplicación Express.

express.text() es una función de middleware integrada en Express.js, un popular framework web de Node.js. Analiza las cargas útiles de las solicitudes entrantes en una cadena y se basa en el middleware body-parser

El middleware urlencoded() de Express.js se utiliza para analizar solicitudes entrantes con cargas útiles codificadas en URL. Es una función de middleware integrada que analiza el cuerpo de la solicitud como datos codificados en URL y completa el objeto req.body con los datos analizados. La opción **extended** permite la inclusión de objetos anidados en los datos analizados. Si se establece en falso, solo se analizarán pares clave-valor planos. El middleware urlencoded solo analiza las solicitudes con el encabezado Content-Type establecido en application/x-www-form-urlencoded. Si el encabezado no está presente o está establecido en un valor diferente, el middleware no analizará el cuerpo de la solicitud.

En Express.js 4.16.0 y versiones posteriores, el middleware body-parser ya no es necesario y se puede utilizar en su lugar el middleware urlencoded integrado.


## ejemplo con variabls de entorno

Usaremos un archivo .env. 
Cree archivo: .env

Archivo: .env
```js
PORT=3000
```
Cargue la biblioteca dotenv
```sh
npm i dotenv
```

Código del ejemplo
```js
import express from "express"
import dotenv from 'dotenv'

dotenv.config() //cargar las variables de entorno del archivo .env en process.env
const PORT=process.env.PORT || 3000 //cargar el numero de puerto

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

midleware para ruta no encontrada, poner al final (antes del listen):

```js
// Middlewares
app.use((_, res, next) => {
  res.status(404).send("404 página no encontrada");
});
```

## manejo de directorio path

process.cwd() es un método de Node.js que devuelve el directorio de trabajo actual del proceso de Node.js. Proporciona la ruta absoluta del directorio desde el que se inició el proceso de Node.js. Este directorio se suele denominar “directorio de trabajo actual” o “CWD”

```js
process.cwd() //devuelve el directorio de trabajo corriente del proceso de Node.js
```

Prácticas recomendadas:

Use process.cwd() para construir rutas de archivos y garantizar la coherencia de la plataforma.
Tenga en cuenta el comportamiento de los enlaces simbólicos y los posibles problemas con la distinción entre mayúsculas y minúsculas en determinadas plataformas.
Pruebe su código en diferentes plataformas para garantizar la compatibilidad.
Al comprender process.cwd() y su comportamiento, puede escribir aplicaciones Node.js más sólidas e independientes de la plataforma.

## estructura de carpetas

mi-proyecto-express/
├── node_modules/   # la crea npm
├── package.json    # archivo de configuracion lo crea npm
├── app.js          # Punto de entrada
├── routes/         # Rutas (ej: users.js, products.js)
├── controllers/    # Lógica de las rutas
├── middleware/     # Middlewares personalizados
└── public/         # Archivos estáticos (CSS, JS, imágenes)

## crear proyectos
usando modulos common js
[crear proyectos con express](https://expressjs.com/es/starter/generator.html)

## crar proyectos (ok)
Para crear un proyecto node con express puede tambien usar el generador de proyectos:
```sh
#instalar el genrador de proyectos
npm install -g express-generator@4
# crear el proyecto por ejemplo con el motor de vsitas ejs
express nodeServer --view=ejs
cd nodeSerever
npm install
npm run start
```
con run start: node ./bin/www
o: node --env-file=.env ./bin/www

Se recomienda vite

## cors

```js
import cors from 'cors'
const corsOptions={
    origin:"http://127.0.0.1:5173", //especificar algun origen
    methods:["POST","GET"],
    credentials: true //allow sending credentials (cookies, authentication)
}

app.use(cors(corsOptions))
```
# refs

[sesiones](https://ull-esit-dsi-1617.github.io/estudiar-cookies-y-sessions-en-expressjs-alejandro-raul-35l2-p4/sessionsexpress.html)

[Con express](https://www.npmjs.com/package/express)

[Crear proyecto express](https://www.npmjs.com/package/express-create-app)