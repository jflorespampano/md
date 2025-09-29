---
categoría: programación
tipo: js
tags:
---
# sesiones

En Express.js, las sesiones son un mecanismo para almacenar información del usuario entre diferentes peticiones HTTP. A diferencia de las cookies (que se guardan en el cliente), las sesiones suelen almacenarse en el servidor y se asocian a un ID único (generalmente guardado en una cookie en el cliente).

¿Para qué sirven las sesiones?
* Mantener el estado de un usuario (ej: login, carrito de compras).

* Almacenar datos temporales de forma segura en el servidor.

* Evitar enviar información sensible en cada petición.

## como implementar sesiones en express

```sh
npm install express-session
```

Configuración básica:

```js
const express = require('express');
const session = require('express-session');

const app = express();

// Configuración de sesión
app.use(session({
  secret: 'miClaveSecreta',  // Clave para firmar la cookie (¡debe ser segura!)
  resave: false,             // Evita guardar la sesión si no hay cambios
  saveUninitialized: false,  // Evita guardar sesiones vacías
  cookie: { secure: false }  // En producción usa 'secure: true' (HTTPS)
}));

// Ruta de ejemplo que usa la sesión
app.get('/', (req, res) => {
  // Guardar datos en la sesión
  req.session.usuario = 'JuanPerez';
  req.session.visitas = (req.session.visitas || 0) + 1;

  res.send(`Hola ${req.session.usuario}, visitas: ${req.session.visitas}`);
});

app.listen(3000, () => console.log('Servidor en http://localhost:3000'));
```

## Almacenamiento de sesiones

Por defecto, express-session guarda las sesiones en memoria, pero esto no es recomendado para producción. Usa almacenamientos externos:

1. Con connect-redis (para Redis)

```sh
npm install connect-redis redis
```
```js
const RedisStore = require('connect-redis')(session);
const redisClient = require('redis').createClient();

app.use(session({
  store: new RedisStore({ client: redisClient }),
  secret: 'claveSecreta',
  resave: false,
  saveUninitialized: false
}));
```
2. Con connect-mongodb-session (para MongoDB)

```sh
npm install connect-mongodb-session
```

```js
const MongoDBStore = require('connect-mongodb-session')(session);
const store = new MongoDBStore({
  uri: 'mongodb://localhost:27017/miBasedeDatos',
  collection: 'sesiones'
});

app.use(session({
  store: store,
  secret: 'claveSecreta',
  resave: false,
  saveUninitialized: false
}));
```

## como verificar si un usuario tiene sesion activa

```js
// Middleware para verificar sesión
function checkAuth(req, res, next) {
  if (req.session.usuario) {  // Si existe 'usuario' en la sesión
    next();  // Usuario autenticado, continúa
  } else {
    res.redirect('/login');  // Redirige al login si no hay sesión
  }
}

// Uso en una ruta protegida
app.get('/perfil', checkAuth, (req, res) => {
  res.send(`Bienvenido ${req.session.usuario.nombre}`);
});
```

## Ejemplo 1 (login, logout) de (deep seek)

archivo: app.js
```js
const express = require('express');
const session = require('express-session');

const app = express();

app.use(session({
  secret: 'tu_clave_secreta',
  resave: false,
  saveUninitialized: false,
  cookie: { maxAge: 3600000 } // Sesión expira en 1 hora
}));

//rutas de autenticación
// Login (establece la sesión)
app.post('/login', (req, res) => {
  // Aquí validarías credenciales con tu DB
  req.session.usuario = { 
    id: 123, 
    nombre: 'Ejemplo',
    email: 'usuario@example.com'
  };
  res.send('Sesión iniciada');
});

// Logout (destruye la sesión)
app.get('/logout', (req, res) => {
  req.session.destroy(err => {
    if (err) return res.send('Error al cerrar sesión');
    res.redirect('/login');
  });
});

// Ruta protegida
app.get('/dashboard', (req, res) => {
  if (!req.session.usuario) {
    return res.status(401).send('Acceso no autorizado');
  }
  res.send(`Panel de control - Hola ${req.session.usuario.nombre}`);
});

//uso en rutas
const { isLoggedIn } = require('./authMiddleware');

app.get('/api/privada', isLoggedIn, (req, res) => {
  res.json({ data: 'Información secreta' });
});

//verificación en vistas, Si usas plantillas, pasa el estado de la sesión al frontend:
app.get('/', (req, res) => {
  res.render('index', { 
    user: req.session.usuario || null 
  });
});
```
archivo:authMiddleware.js
```js
//middleware
module.exports = {
  isLoggedIn: (req, res, next) => {
    if (req.session.usuario) {
      next();
    } else {
      res.status(403).json({ error: 'Debes iniciar sesión' });
    }
  }
};
```

Plantilla ejs: index.ejs
```html
<% if (user) { %>
  <p>Bienvenido <%= user.nombre %></p>
<% } else { %>
  <a href="/login">Iniciar sesión</a>
<% } %>
```


## Ejemplo 2 de Sessions en ExpressJS

Autentificación: Es el proceso por el cual se verifica que el usuario es quien él dice ser.
Autorización: Es el proceso de determinar si el usuario tiene permisos para acceder a los datos o archivos que el ha solicitado.
A continuación se le mostrará un ejemplo muy sencillo de una autentificación y una autorización usando session in express.js. Hay un punto para loguearte y un punto para desloguearte y un método get que te muestra la página. Para ver la página publicada deberás estar logueado primero, además tu identidad será verificada y guardada en dicha sesión. Cuándo te desloguees de la página sucederá que: te rechazará el acceso borrando tu identidad de la sesión.

```js
var express = require('express'),
    app = express(),
    session = require('express-session');
app.use(session({
    secret: '2C44-4D44-WppQ38S',
    resave: true,
    saveUninitialized: true
}));

// Authentication and Authorization Middleware
var auth = function(req, res, next) {
  if (req.session && req.session.user === "amy" && req.session.admin)
    return next();
  else
    return res.sendStatus(401);
};

// Login endpoint
app.get('/login', function (req, res) {
  if (!req.query.username || !req.query.password) {
    res.send('login failed');    
  } else if(req.query.username === "amy" || req.query.password === "amyspassword") {
    req.session.user = "amy";
    req.session.admin = true;
    res.send("login success!");
  }
});

// Logout endpoint
app.get('/logout', function (req, res) {
  req.session.destroy();
  res.send("logout success!");
});

// Get content endpoint
app.get('/content', auth, function (req, res) {
    res.send("You can only see this after you've logged in.");
});

app.listen(3000);
console.log("app running at http://localhost:3000");
```

Para probar el código pondríamos en la línea de comandos:

```sh
npm install express
npm install express-session
node session_auth.js &
# ademas visitar las url
localhost:3000/content
localhost:3000/login?username=amy&password=amyspassword
localhost:3000/content
localhost:3000/logout
localhost:3000/content
```

## ejemplo deep seek numero 2

mi-proyecto/
├── server.js
├── package.json
└── views/
    └── index.ejs


```js
const express = require('express');
const session = require('express-session');
const mongoose = require('mongoose');
const MongoStore = require('connect-mongodb-session')(session); // Opcional: para MongoDB

const app = express();

// Configuración de sesión (en memoria)
app.use(session({
  secret: 'mi-clave-secreta-123', // Cambia esto en producción
  resave: false,
  saveUninitialized: false,
  cookie: { 
    maxAge: 1000 * 60 * 60 * 24, // 1 día de duración
    secure: false // En producción usa 'true' (HTTPS)
  }
}));

// Middleware para verificar sesión
const requireLogin = (req, res, next) => {
  if (!req.session.user) {
    return res.redirect('/login');
  }
  next();
};

// Rutas
app.get('/', (req, res) => {
  res.send(`
    <h1>Home</h1>
    ${req.session.user 
      ? `<p>Bienvenido ${req.session.user.name} | <a href="/logout">Cerrar sesión</a></p>`
      : '<a href="/login">Iniciar sesión</a>'
    }
  `);
});

app.get('/login', (req, res) => {
  // Simulamos autenticación exitosa
  req.session.user = {
    id: 1,
    name: 'Juan Pérez',
    email: 'juan@example.com'
  };
  res.redirect('/dashboard');
});

app.get('/dashboard', requireLogin, (req, res) => {
  res.send(`
    <h1>Dashboard</h1>
    <p>Sesión activa para: ${req.session.user.name}</p>
    <a href="/">Volver al home</a>
  `);
});

app.get('/logout', (req, res) => {
  req.session.destroy(err => {
    if (err) console.error(err);
    res.redirect('/');
  });
});

// Iniciar servidor
app.listen(3000, () => {
  console.log('Servidor en http://localhost:3000');
});
```

versión con mongo db
```js
// Añade esto después de 'const app = express()'
const store = new MongoStore({
  uri: 'mongodb://localhost:27017/mi-base-de-datos',
  collection: 'sessions'
});

app.use(session({
  store: store, // Usa MongoDB para almacenar sesiones
  // ... resto de la configuración igual
}));

// Conectar a MongoDB
mongoose.connect('mongodb://localhost:27017/mi-base-de-datos')
  .then(() => console.log('Conectado a MongoDB'))
  .catch(err => console.error(err));
```

instalación de dependencias
```sh
npm install express express-session 
# Opcional para MongoDB:
npm install mongoose connect-mongodb-session
```
## ligas

Ejemplo anterior:
[ref](https://ull-esit-dsi-1617.github.io/estudiar-cookies-y-sessions-en-expressjs-alejandro-raul-35l2-p4/sessionsexpress.html)

[ejemplo](https://github.com/blog-johnserrano/express-sessions/tree/master)
[explicación del ejemplo anyterior](https://johnserrano.co/blog/manejo-de-sesiones-con-express)
