## instalar json-server SERVIDOR JSON LOCAL

JSON Server es un módulo de Node.js que permite crear un servidor json web con una API REST al instante para su uso en aplicaciones cliente, como aplicaciones web o móviles.
Para instalar JSON Server globalmente, puede usar uno de los siguientes comandos.

```sh
npm install -g json-server
# or if you use pnpm
pnpm install -g json-server
```

```sh
# instalar json-server
npm i json-server
``` 

crear un archivo json, pej: en la carpeta db: db/products.jon con los datos
```js
{
    "products":[
        {
            "id":1,
            "name":"laptop",
            "description":"laptop gaming",
            "price":1000,
            "inStock":true
        }
        //...resto de los datos
    ]
}
```
Agrear al package.json, en la  lista de scripts, la entrada:

```json
"back": "json-server db/products.json --port 3000"
```

puede arrancar el servidor json así:
```sh
npm run back
```

Listo en el puerto 3000 se tiene un servidor que devuelve datos json.
se consulta así:
```
http://localhost:3000/products
http://localhost:3000/products/1
```

### json-server con npx

```sh
# ejecutar json-server con npx
npx json-server data.json -p 3000
```

## Refs

[ref](https://www.npmjs.com/package/json-server)