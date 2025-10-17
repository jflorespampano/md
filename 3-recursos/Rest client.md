
Agregue a sus complementos  de VsCode, el complemento {Rest Client} del autor: Huachao Mao
## Ejemplo

```http
# archivo: consultas.http
GET https://jsonplaceholder.typicode.com/posts HTTP/1.1
  
###
  
POST https://jsonplaceholder.typicode.com/posts HTTP/1.1
content-type: application/json
  
{
    "id":"23",
    "nombre":"ana perez",
    "correo":"ana@mail",
    "edad":32
}
```
Al pasar el ratón por la sentencia get o post le aparece una opción para lanzar la consulta.
