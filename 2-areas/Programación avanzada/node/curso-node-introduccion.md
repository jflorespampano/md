---
categoría: programación
tipo: js
---
# Programación en Node

Node.js es un entorno de ejecución de JavaScript multiplataforma y de código abierto. ¡Es una herramienta popular para prácticamente cualquier tipo de proyecto!

Node.js ejecuta el motor JavaScript V8, el núcleo de Google Chrome, fuera del navegador. Esto le permite alcanzar un alto rendimiento.

Una aplicación Node.js se ejecuta en un solo proceso, sin crear un nuevo hilo para cada solicitud. Node.js proporciona un conjunto de primitivas de E/S asíncronas en su biblioteca estándar que evitan el bloqueo del código JavaScript. Además, las bibliotecas de Node.js generalmente se escriben utilizando paradigmas no bloqueantes. Por lo tanto, el comportamiento bloqueante es la excepción y no la norma en Node.js.

Cuando Node.js realiza una operación de E/S, como leer de la red, acceder a una base de datos o al sistema de archivos, en lugar de bloquear el hilo y perder ciclos de CPU esperando, Node.js reanuda las operaciones al recibir la respuesta.

Esto permite a Node.js gestionar miles de conexiones simultáneas con un solo servidor sin la carga de gestionar la concurrencia de hilos, lo cual podría ser una fuente importante de errores.

Node.js tiene una ventaja única: millones de desarrolladores frontend que escriben JavaScript para el navegador ahora pueden escribir el código del lado del servidor, además del código del lado del cliente, sin necesidad de aprender un lenguaje completamente diferente.

En Node.js, los nuevos estándares ECMAScript se pueden utilizar sin problemas, ya que no es necesario esperar a que todos los usuarios actualicen sus navegadores. Usted decide qué versión de ECMAScript usar modificando la versión de Node.js, y también puede habilitar funciones experimentales específicas ejecutando Node.js con indicadores.

## Ejemplo servidor web node

```js
import { createServer } from 'node:http';

const hostname = '127.0.0.1';
const port = 3000;

const server = createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```
## referencias

[Referencia Node](https://nodejs.org/es)



