---
categoría: programación
tipo: js
tags:
  - sqlite
---

# better-sqlite3

La biblioteca más rápida y sencilla para SQLite3 en Node.js. Soporte completo para transacciones. Alto rendimiento, eficiencia y seguridad. API sincrónica fácil de usar (mejor concurrencia que una API asincrónica... sí, leyó bien). Soporte para funciones definidas por el usuario, agregados, tablas virtuales y extensiones. Enteros de 64 bits (invisibles hasta que los necesite). Soporte para subprocesos de trabajo (para consultas grandes/lentas).

```sh
#instalar
npm install better-sqlite3
```

## crear db

```js
//Archivo crearTabla.js
import Database from "better-sqlite3";
const db = new Database('app.db')

const query=`CREATE TABLE users(
    id INTEGER PRIMARY KEY,
    name STRING NOT NULL,
    username STRING NOT NULL UNIQUE
)    
`
db.exec(query)
db.close()
```

Insertar datos
```js
//Archivo insertaDatos
import Database from "better-sqlite3";
const db = new Database('app.db')

const data=[
    {name:"ana",username:"an1"},
    {name:"juan",username:"ju2"},
    {name:"bety",username:"be3"},
    {name:"paco",username:"pa0"},
    {name:"luis",username:"lu5"}
]
const insertData=db.prepare(`insert into users(name,username) values(?,?)`)

data.forEach(user=>{
    const r=insertData.run(user.name, user.username)
    console.log(r)
})
db.close()
```
Salida:
```txt
[
  { id: 1, name: 'ana', username: 'an1' },
  { id: 2, name: 'juan', username: 'ju2' },
  { id: 3, name: 'bety', username: 'be3' },
  { id: 4, name: 'paco', username: 'pa0' },
  { id: 5, name: 'luis', username: 'lu5' }
]
```

Consultar todos:
```js
//Archivo:consultaTodos.js
import Database from "better-sqlite3";
const db = new Database('app.db')

const query = "select * from users;"
const users = db.prepare(query).all()
db.close()

console.log(users)
```

Consulta uno
```js
//Archivo:consultaUno.js
import Database from "better-sqlite3";
const db = new Database('app.db')

const query = "select * from users where id=?;"
const users = db.prepare(query).get(1)
db.close()

console.log(users)
```

## con modelo DAO

Controlador: Archivo DaoBetterSqlite3.js
```js
import Database from "better-sqlite3";

class AppDaoBetterSQLite{
    constructor(dbFilePath){
        this.dbName=dbFilePath
        this.db=null
        this.dbOpen=false
    }
    open(){        
        this.db = new Database(this.dbName)
        this.dbOpen=true
    }
    run(sql, params = []) {
        const insertData = this.db.prepare(sql)
        const r=insertData.run(params)
        return r
    }
    get(sql, params = []) {
        //si la consulta fue satisfactoria pero no hay datos  devuelve undefined 
        const res = this.db.prepare(sql).get(params)
        return res
    }

    all(sql, params = []) {
        const res = this.db.prepare(sql).all()
        return res
    }
    close(){
        console.log("base de datos cerrada")
        if(this.dbOpen) this.db.close()
    }
}


export default AppDaoBetterSQLite
```

Modelo: Archivo model.users.js

```js
class ModelUsers{
    constructor(controller){
        this.dbController=controller
    }
    /**
     * 
     * @param {*} id entero que representa el id
     * @returns 
     */
    get(id){
        const sql=`select * from users where id=?;`
        this.dbController.open()
        const data = this.dbController.get(sql,[id])
        this.dbController.close()
        return data
    }
    /**
     * Devuelve la lista de todos los usuarios
     * @returns objeto con la lista de datos
     */
    getAll(){
        const sql=`select * from users;`
        this.dbController.open()
        const data = this.dbController.all(sql,[])
        this.dbController.close()
        return data
    }
    /**
     * Inserta un registro en users
     * @param {*} datos arreglo de parametros [name,username]
     * @returns 
     */
    insert(datos){
        const sql='insert into users(name,username) values(?,?)'
        this.dbController.open()
        const data = this.dbController.run(sql,datos)
        this.dbController.close()
        return data
    }

    //agregue el método put para actualizar todos los campos de un registro
    //agregue patch para actualizar un campo específico
    //agregue delete para borrar un registro
}
export default ModelUsers
```

Ejemplo de uso: Archivo DaoBetterSqlite3.js

```js
//usar Dao
import AppDaoBetterSQLite from './DaoBetterSqlite3.js'
import ModelUsers from "./model.users.js";

const controllerDB=new AppDaoBetterSQLite('app.db')
const mc=new ModelUsers(controllerDB)

// const resp=mc.getAll()
const resp= mc.get(3)
console.log(resp)

```


## refs

[sitio](https://www.npmjs.com/package/better-sqlite3)
