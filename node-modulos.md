En ES% (ECMAScrpt15) define una implementacion estandar para los modulos
|       Uso        | sintaxis|
|------------------|---------|
|importar un modulo completo           | import * as name from ‘module-name’ |
|importar el default export de 1 modulo| import name from ‘module-name’ |
|importar una exportacion unica | import { name } from ‘module-name’ |
|importar multiples exportaciones | import { nameOne , nameTwo } from ‘module-name’ |
|importar un modulo solo para efectos laerales| import ‘./module-name’ |


## Puede usar los modulos ES6 cambiando el package.json

Para acivar el uso de modulos ES6 agregue la línea siguiente al package.json:

"type":"module"

### ejemplo crear servidor express con modulos

```js
//index.js

import express from 'express';
const app = express();

app.get('/', (req, res) => {
	res.send('GeeksforGeeks');
})
const PORT = 5000;

app.listen(PORT, () => {
	console.log(`Running on PORT ${PORT}`);
})

```


## notas
