## CORS

Para aceptar intercambio de recursos de origen cruzado (CORS), en PHP debe poner al inicio de su script las siguientes 3 lineas:

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

### Ejemplo:

Suponga que tiene una BD en SQLite3 llamada partes con una lista de partes con camopps como: (id, nombre, existencia), para acceder a estos desde php y poder ejecutar el script php desde un origen cruzado, haría:

Archivo: getPartes.php
```php
<?php
header('Access-Control-Allow-Origin: *');
header("Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept");
header('Access-Control-Allow-Methods: GET, POST, PUT, DELETE');
$conex = new PDO("sqlite:" . __DIR__ . "/provpar.sqlite3");
$conex->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

$stmt = $conex->prepare('SELECT * FROM partes;');
$r=$stmt->execute();

if ($r) { 
    http_response_code(200);
    $data = $stmt->fetchAll(PDO::FETCH_ASSOC);
    $respuesta=[
        "sucess"=>"true",
        "data"=>$data,
        "error"=>""
    ];
    echo(json_encode($respuesta));
	
}else{
    http_response_code(400);
    echo(json_encode([
        "sucess"=>"false",
        "data"=>[],
        "error"=>""
    ]));
}
// echo json_encode($data);

?>
```
llamar desde un origen distinto:

```js
fetch('getPartes.php')
.then(response=>response.json())
.then((datos)=>{
    console.log("items=",datos.data)
})
.catch(err=>{
    console.log(err)
})
```