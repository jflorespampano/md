# Recomendaciones

Para tener una organización en su directorios(carpetas), se recomienda crear la siguiente estrcutura:

Dentro de la carpeta:
<pre>
C:\Users
</pre>
o dentro de
<pre>
C:\Users\suUsuario
</pre>

Cree las carpetas:

<pre>
C:\Users\suUsuario\web\github.com\suUsuarioDeGitHub
C:\Users\suUsuario\node
C:\Users\suUsuario\trabajo
</pre>

C:\Users\suUsuario\trabajo la usaremos para realizr las pruebas de aprendizaje.

C:\Users\suUsuario\node la usara para almacenar sus ejercicios del curso.

C:\Users\web\github.com\suUsuarioDeGitHub para sus proyetos web que querramos subir a GitHub.

## Puede optar por trabajar con esta estructura:

<pre>
C:\trabajo
C:\trabajo\web\github.com\suUsuarioDeGitHub
C:\trabajo\node
</pre>

Donde en la carpeta: C:\trabajo\node

pone sus ejemplos de código del curso

Y en la carpeta:C:\trabajo\web\github.com\suUsuarioDeGitHub

Pone los proyectos que seran respaldados en gitHub

## Estructura de carpetas para un proyecto

Si esta trabajando con la estrcutura:
(por ejemplo en mi caso):

C:\trabajo\web\jflorespampano@gmail.com

Cada proyecto a ser respaldado en gitHub sera una carpeta dentro de esta:

<pre>
C:\trabajo\web\jflorespampano@gmail.com
                    ├── proyecto1
                    ├── proyecto2
                    └── proyecto3
</pre>

A su vez cada proyecto tendrá su propia estructura
 
### proyecto node/ express

Puede usar alguna de lar siguientes herramientas para crear la estructura de carpetas de su proyecto:

1. [herramienta generator:](https://expressjs.com/es/starter/generator.html)


2. usando modulos common js
[crear proyectos con express](https://expressjs.com/es/starter/generator.html)

3. La que usaremos en el curso:

El comando npm install -g express-generator@4 se utiliza para instalar globalmente la herramienta Express Generator (versión 4.x), que te permite crear rápidamente la estructura básica de un proyecto backend con Express.js en Node.js.
Crear un proyecto node con express 
```sh
#instalar el genrador de proyectos
npm install -g express-generator@4
# crear el proyecto por ejemplo con el motor de vsitas ejs
express nodeServer --view=ejs
cd nodeSerever
npm install
npm run start
```

Opciones:
--view=ejs: Opcional. Define el motor de plantillas (puedes usar pug o hbs).
nodeServer: Nombre de tu carpeta/proyecto.

Ahora con run start: node ./bin/www
o: node --env-file=.env ./bin/www

4. [Con express](https://www.npmjs.com/package/express)

5. [Crear proyecto express](https://www.npmjs.com/package/express-create-app)

O puede crear su estructura a mano de otra forma; puede ser:
<pre>
.
├── .env
├── controllers
│   └── persona.controller.js
├── src
│   ├── css
│   └── js
├── middlewares
├── models
│   └── persona.model.js
├── package.json
├── routes
│   ├── persona.route.js
│   └── materia.route.js
├── server.js
└── views
    ├── error.pug
    ├── index.pug
    └── layout.pug
</pre>

Estructura de carpetas segun Deep Seek

<pre>
mi-backend/
├── src/
│   ├── controllers/       # Lógica de manejo de rutas
│   │   ├── userController.js
│   │   └── authController.js
│   ├── routes/            # Definición de rutas
│   │   ├── userRoutes.js
│   │   └── authRoutes.js
│   ├── models/            # Modelos de base de datos (Mongoose/SQL)
│   │   ├── User.js
│   │   └── Product.js
│   ├── services/          # Lógica de negocio (opcional)
│   │   ├── userService.js
│   │   └── authService.js
│   ├── middlewares/       # Middlewares personalizados
│   │   ├── authMiddleware.js
│   │   └── errorHandler.js
│   ├── utils/             # Utilidades (helpers, config)
│   │   ├── logger.js
│   │   └── database.js
│   ├── config/            # Configuraciones (env, constants)
│   │   ├── env.js
│   │   └── cloudinary.js
│   ├── public/            # Archivos estáticos (images, CSS)
│   └── app.js             # Configuración principal de Express
├── tests/                 # Pruebas unitarias/integración
│   ├── user.test.js
│   └── auth.test.js
├── .env                   # Variables de entorno (NO subir a Git)
├── .gitignore             # Ignorar node_modules, .env, etc.
├── package.json           # Dependencias y scripts
└── server.js              # Punto de entrada (inicia el servidor)
</pre>

## ligas

[Estructuras de carpetas](https://www.webreactiva.com/blog/organizar-estructura-proyecto-incremental)