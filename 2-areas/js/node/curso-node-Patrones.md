---
categoría: programación
tipo: js
---
# ejemplo de aplicación api con node usando patrones

# Iniciar proyecto

```sh
#inicar proyecto
npm init -y
#cargar dependencias
npm i dotenv --save
npm i express
npm i sqlite3
```
## Crear el archivo config
En su carpeta raiz creé el archivo '.env'
archivo '.env'
```json
PORT=3000
DB_PLATFORM="sqlite"
SQLITE3_DB_NAME="dataBase.sqlite"
SQLITE3_DB_MEMORY=":memory:"
MYSQL_HOST=""
MYSQL_DB_NAME=""
MYSQL_USER=""
MYSQL_PASSWORD=""
URL="http://localhost"
```
En este pondrá las variables de ambiente de su proyecto

## caargar archivo .env
Para acragar las variables de ambiente del archivo '.env' a su proyecto haga:

En su archivo: index.js
```js
const dotenv =require('dotenv')

dotenv.config() //carga variables del archivo .env, y se accede así:
const DB_PLATFORM=process.env.DB_PLATFORM
console.log(DB_PLATFORM)

```
Pruebe este código: `node index.js`

## Patron DAO

Vamos a implementar el patron DAO, este patron abstrae la implementación de la base de datos, para esto debemos saber que las clases abstractas en js no existen sin embargo vamos a simularlas así:

Necesitamos una clase generica para cualquier gestor de base de datos (sqlite, mysql, pstgresql) e independientemente del gestor de bd definiremos un conjunto de operaciones, tales como:

* open abre la base de datos
* run ejecuta una sentencia sql, la usaremos para insert, delete, update, create table
* get devuelve un registro, la usaremos para select where
* all devuelve todos los registros, la usaremos para select
* close cierra la base de datos

Nuestra clase generica es:

Archivo: Dao.js
```js
class Dao{
    constructor(db_host='',db_name='',db_user='',db_pass='',dbFilePath=''){
        this.db_host=db_host
        this.db_name=db_name
        this.db_user=db_user
        this.db_pass=db_pass
        this.dbFilePath=dbFilePath
        this.dbOpen=false
        this.db=null
    }
    open(){
        throw new Error("open() debe ser implementado")
    }
    run(sql, params = []) {
        throw new Error("run() debe ser implementado")
    }
    get(sql, params = []) {
        throw new Error("get() debe ser implementado")
    }

    all(sql, params = []) {
        throw new Error("all() debe ser implementado")
    }
    close(){
        throw new Error("close() debe ser implementado")
    }
}

module.exports = Dao
```

## Implementar DAO para sqlite
Ahora implementamos la funcionalidad enterior para sqlite:

Creé el archivo DaoSqlite.js así:
```js
//dao para sqlite
const dao=require('./Dao.js')
const sqlite3 =require('sqlite3').verbose()

class AppDao extends dao{
    constructor(dbFilePath){
        super('','','','',dbFilePath)
    }
    open(){
        return new Promise((resolve, reject)=>{
            this.db = new sqlite3.Database(this.dbFilePath, (err) => {
                if (err) {
                    console.log('No se pudo conectar a la database: ', err)
                    this.dbOpen=false
                    reject("La base de datos no se pudo abrir")

                } else {
                    console.log('Connectado a la database')
                    this.dbOpen=true
                    resolve(true)
                }
            })
        })
    }
    run(sql, params = []) {
        // console.log(sql,params)
        return new Promise((resolve, reject) => {
            this.db.run(sql, params, function (err) {
                if (err) {
                    console.log('Error corriendo  sql ' + sql)
                    console.log(err)
                    reject("en run ",err)
                } else {
                    //si el statemet se ejcuta satisfactoriamente
                    //el objeto this contiene 2 propiedades:
                    //lastID contiene el inidce del ultimo registro insertado.
                    //changes contiene el indice del ultimo renglon afectado por la consulta.
                    //console.log("en run ",{ id: this.lastID, changes: this.changes })
                    // console.log({ id: this.lastID, changes: this.changes })
                    resolve({ id: this.lastID, changes: this.changes })
                }
            })
        })
    }
    get(sql, params = []) {
        return new Promise((resolve, reject) => {
            this.db.get(sql, params, (err, result) => {
                if (err) {
                    console.log('Error running sql: ' + sql)
                    console.log(err)
                    reject(err)
                } else {
                    //console.log(`consulta ${sql} correcta `,result)
                    resolve(result)
                    //resolve({ id: this.lastID, changes: this.changes })
                }
            })
        })
    }

    all(sql, params = []) {
        return new Promise((resolve, reject) => {
            this.db.all(sql, params, (err, rows) => {
                if (err) {
                    console.log('Error running sql: ' + sql)
                    console.log(err)
                    reject(err)
                } else {
                    resolve(rows)
                }
            })
        })
    }
    close(){
        console.log("base de datos cerrada")
        if(this.dbOpen) this.db.close()
    }
}

module.exports = AppDao
```

De manera similar implementamos las clases para otros gestores de bases de datos

La manera de probar hasta ahora es poner este código en su archivo index.js

Archivo: index.js
```js
const sqlite=require('./DaoSqlite.js')

const db=new sqlite('prueba.sqlite3')

db.open()
.then(()=>{
    return db.all('select * from persona')
})
.then((data)=>{
    console.log(data)
})
.catch((error)=>{
    console.log(error)
})
```
## Patron factory
Este nos servirá para generar el objeto adecuado según el manejador de base de datos que definimos en .env, en la variable DB_PLATFORM.

Archivo: factoryDao.js
```js
const AppDaoSqlite = require("./DaoSqlite.js")
const AppDaoMysql = require("./DaoMysql.js")
const dotenv =require('dotenv')

dotenv.config()

//patron factory para devolver el dbms adecuado:
function getDAO(){
    if(DB_PLATFORM === "sqlite"){
        //crear obejto de sqlite
        console.log("ES Sqlite")
        //variables no usadas en sqlite
        // const MYSQL_HOST=""
        // const MYSQL_DB_NAME=""
        // const MYSQL_USER=""
        // const MYSQL_PASSWORD=""
        const SQLITE3_DB_NAME=process.env.SQLITE3_DB_NAME
        return new AppDaoSqlite(SQLITE3_DB_NAME)
    }else if(DB_PLATFORM === "mysql"){
        //crear objeto de mysql
        console.log("es Mysql")
        // const MYSQL_HOST=process.env.MYSQL_HOST
        // const MYSQL_DB_NAME=process.env.MYSQL_DB_NAME
        // const MYSQL_USER=process.env.MYSQL_USER
        // const MYSQL_PASSWORD=process.env.MYSQL_PASSWORD
        // return new AppDaoMysql(DB_HOST,DB_NAME,DB_USER,DB_PASS)
        return null
    }
}
module.exports = getDAO
```

Ahora probamos así:
Archivo: index.js

```js
const getDao=require("./factoryDao.js")
const dao=getDao()
dao.open()
.then(()=>{
    return db.all('select * from persona')
})
.then((data)=>{
    console.log(data)
})
.catch((error)=>{
    console.log(error)
})
```