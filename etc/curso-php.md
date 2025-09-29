# php

## Uso de core

[cors php](https://victorroblesweb.es/2017/04/23/cabeceras-http-php-permitir-acceso-cors/)

[Ejemplo de cors php](https://desarrolloweb.com/articulos/solucion-problemas-api-php-cors-post.html)
```php
header('Access-Control-Allow-Origin: *');
header("Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept");
header('Access-Control-Allow-Methods: GET, POST, PUT, DELETE');
```
Resumimos ahora las cabeceras implicadas, para que tengas algo más de información.
Access-Control-Allow-Origin

En la primera cabecera estamos diciendo que se permita el acceso a los recursos desde cualquier origen (cualquier dominio, aunque se podría especificar sobre qué dominios en particular, si es que solo queremos permitir el acceso desde determinados dominios).

Esta primera cabecera es la más importante y la que primeramente percibirás que te está faltando. En su ausencia, el navegador te marcará el siguiente error: "Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource."
Access-Control-Allow-Headers

La segunda dice que se acepten diversos content-type, como el "application/json" que usan los frameworks habitualmente.

Esta cabecera también es fundamental y si no la colocas el navegador te lo marcará con el el error: "Request header field content-type is not allowed by Access-Control-Allow-Headers in preflight response"
Access-Control-Allow-Methods

La tercera dice que se permitan diversos métodos de conexión que se suelen usar la comunicación con el servicio web, para las distintas operaciones del API. Estos son GET, POST, PUT y DELETE.

Esta tercera cabecera en principio parece que no es necesaria, ya que el servidor permite el acceso con métodos como POST de manera predeterminada, pero nunca está de más indicarlo en tu API. 

## php composer

Inicaiar proyecto
```sh
md carpeta-proyecto
cd carpeta-proyecto
composer init
# responder a las preguntas/tomar el default en dependencias dar n
composer install
ir a la carpeta padre del proyecto y crear el servidor
php -S localhost:8080 -t carpaeta-proyecto
#instalar el router de php (bramus/router)
composer require bramus/router ~1.6
#agregar rutas:
```

agregar las rutas al archivo index.php
```php
<?php
// Require composer autoloader
require __DIR__ . '/vendor/autoload.php';

// Create Router instance
$router = new \Bramus\Router\Router();

// Define routes
// ...
// This route handling function will only be executed when visiting http(s)://www.example.org/about
$router->get('/', function() {
    echo 'hola Contents';
});
// Run it!
$router->run();
?>
```

## ORM
descargar readbeans : [readbeans/all-drivers](https://redbeanphp.com/index.php?p=/download)
la carpeta que bajo : RedBeanPHP5_7_4 tiene el archivo rb.php, guardelo en la carpeta raiz del proyecto

modificar el erchivo index.php así:
```php
<?php
// Require composer autoloader
require __DIR__ . '/vendor/autoload.php';
require 'rb.php';
R::setup('mysql:host=localhost;dbname=partes','root','');

// Create Router instance
$router = new \Bramus\Router\Router();

// Define routes
// ...
// This route handling function will only be executed when visiting http(s)://www.example.org/about
$router->get('/', function() {
    $partes=R::find('partes');
    //para aceptar origen cruzado
    header('Access-Control-Allow-Origin: *');
    //indicamos que devolvemos json
    header('Content-Type: application/json');
    echo (json_encode(R::exportAll($partes)));
});
// Run it!
$router->run();
?>
```

