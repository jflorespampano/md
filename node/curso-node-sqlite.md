# Usar SQlite

SQLite es una biblioteca en lenguaje C que implementa un motor de base de datos SQL pequeño, rápido, autónomo, de alta confiabilidad y con todas las funciones. SQLite es el motor de base de datos más utilizado en el mundo. SQLite está integrado en todos los teléfonos móviles y la mayoría de las computadoras y viene incluido en innumerables otras aplicaciones que las personas usan todos los días.

## Node SQLite3 vs SQLite

SQLite y SQLite3 suelen usarse indistintamente, pero no son exactamente lo mismo.

SQLite es un sistema de gestión de bases de datos relacionales (RDBMS) autónomo basado en archivos que almacena datos en un solo archivo. Es una biblioteca C que proporciona un motor de base de datos SQL, lo que permite a los desarrolladores crear, modificar y consultar bases de datos. SQLite es un proyecto maduro, ampliamente utilizado y bien mantenido, con una gran comunidad y una extensa documentación.

SQLite3, por otro lado, es una versión específica del proyecto SQLite. SQLite 3.x es una serie de versiones importantes que introdujo mejoras significativas y nuevas características, como:

Ejecución y optimización de consultas mejoradas
Compatibilidad con tipos de datos JSON
Mecanismos de bloqueo y concurrencia mejorados
Mejor compatibilidad con plataformas Windows y macOS
En términos de diferencias, SQLite3 es esencialmente una versión más avanzada y rica en funciones de SQLite. Si está utilizando una versión anterior de SQLite (por ejemplo, SQLite 2.x), la actualización a SQLite3 puede traer beneficios como un mejor rendimiento, nuevos tipos de datos y un control de concurrencia mejorado.

Node.js y SQLite/SQLite3

Cuando se trata de usar SQLite o SQLite3 con Node.js, la principal diferencia radica en la forma en que interactúa con la base de datos:

sqlite3 (paquete npm): este es un enlace de Node.js para SQLite, que proporciona una interfaz de JavaScript para interactuar con bases de datos SQLite. Es un contenedor alrededor de la biblioteca C de SQLite, que le permite usar bases de datos SQLite en sus aplicaciones Node.js. El paquete sqlite3 es compatible con SQLite 3.x y versiones anteriores.
sqlite (paquete npm): este paquete proporciona una interfaz más liviana y minimalista para SQLite, centrándose en las operaciones principales de la base de datos. Está diseñado para usarse con Node.js y es compatible con SQLite 3.x y versiones posteriores.
En resumen:

SQLite es el motor de base de datos subyacente, mientras que SQLite3 es una versión específica del motor con características y rendimiento mejorados.
sqlite3 y sqlite son paquetes de Node.js que proporcionan interfaces para interactuar con bases de datos SQLite, siendo sqlite3 una opción más completa y con más funciones.
Al elegir entre sqlite3 y sqlite, tenga en cuenta lo siguiente:

Si necesita funciones avanzadas como tipos de datos JSON, control de concurrencia o ejecución de consultas mejorada, utilice sqlite3.
Si necesita una interfaz liviana y minimalista para SQLite, utilice sqlite.
Recuerde que ambos paquetes son compatibles con SQLite 3.x y versiones posteriores, por lo que no puede equivocarse con ninguna de las dos opciones si está apuntando a bases de datos SQLite modernas.

El módulo sqlite3 le proporciona dos métodos para controlar el flujo de ejecución de las sentencias. El método serialize() le permite ejecutar sentencias en modo serializado, mientras que el método parallelize() ejecuta las sentencias en paralelo.

## Manejadores de BD visuales para SQLite

1. [sqlite admin](https://sqliteadmin.orbmu2k.de/)
2. [db manager para sqlite](https://sqlitestudio.pl/)


## Crear una base de datos en SQLite

```js
import sqlite3 from 'sqlite3'
let datos = [
    {
        "userId": 1,
        "id": 1,
        "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
        "body": "quia et suscipit\nsuscipit recusandae consequuntur architecto"
    },
    {
        "userId": 1,
        "id": 2,
        "title": "qui est esse",
        "body": "est rerum tempore  molestiae ut reiciendis\nqui aperiam non debitis po nisi nulla"
    }
]

function crearTabla(db) {
    //serialize garantiza que cada comando dentro de serializa se termine 
    //de ejecutar antes de empezar el otro
    db.serialize(() => {
        const sql = `CREATE TABLE IF NOT EXISTS posts(
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            userId INTEGER NOT NULL,
            title TEXT NOT NULL,
            body  TEXT NOT NULL
        ); `
        db.run(sql);

        const stmt = db.prepare("INSERT INTO posts(userId, title, body) VALUES (?,?,?);");
        datos.forEach(e => {
            stmt.run(e.userId, e.title, e.body);
        });

        stmt.finalize();
        //mostrar datos
        db.each("SELECT * FROM posts;", (err, row) => {
            console.log(row.id + ": " + row.title);
        });
    });
    
}

function instanciarDB(fileName='posts.sqlite3'){
    try {
        //abre la base de datos del archivo: posts.sqlite3 ydevuelve un manejador
        const db = new sqlite3.Database(fileName, (err) => {
            if (err) throw new Error("No se pudo abrir la base de datos")
        })
        crearTabla(db)
        db.close()
    } catch (error) {
        console.log("Error:",error)
    }
}

instanciarDB()
```

## Getionar datos de una base de datos usando callback

```js
import sqlite3 from 'sqlite3'
import { open } from 'sqlite'

//para depuracion
sqlite3.verbose();

async function muestra() {
    // open the database
    const db = await open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    });
    const result = await db.all('SELECT * FROM posts');
    db.close();
    console.log(result);
}
async function leerUnDato() {
    const db = await open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    });
    const result = await db.get('SELECT * FROM posts WHERE id = ?', '1')
    db.close();
    console.log(result);
}
async function insertaDato({ id, userId, title, body }) {
    const db = await open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    });
    const sql = `INSERT INTO posts(userId,title,body) VALUES (${userId},'${title}','${body}')`;
    const result = await db.run(sql);
    console.log('resultado:', result);
    db.close();
    muestra();
}

async function actualizaDato({ id, userId, title, body }) {
    const db = await open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    });
    const sql = `update posts set userId=${userId}, title='${title}', body='${body}' where id=${id}`;
    const result2 = await db.run(sql)
    console.log(result2);
    db.close();
    muestra();
}

## Getionar datos de una base de datos usando promesas


/////////////////////////////////////// promesas ///////////////////////////////
function muestraCnPromesa(callback) {
    open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    }).then((db) => {
        db.all('SELECT * FROM posts')
        .then((result) => {
            callback('salida', result);
            // console.log(result);
        })
        .then(() => {
            db.close().then(() => {
                console.log('cerrada la bd');
            });
        });
    });
}

function insertaDatoCnPromesa({ id, userId, title, body }, callback) {
    open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    }).then(db => {
        const sql = `INSERT INTO posts(userId,title,body) VALUES (${userId},'${title}','${body}')`;
        db.run(sql)
        .then(result => {
            callback('****** salida: ', result);
            // console.log(result);
        })
        .then(() => {
            db.close().then(() => {
                console.log('cerrada la bd');
            });
        }).catch(error => {
            console.log('error en la consulta', error);
        });
    }).catch((error) => {
        console.log('error al abrir la bd', error);
    });
}

function actualizaDatoCnPromesa({ id, userId, title, body }) {
    open({
        filename: 'posts.sqlite3',
        driver: sqlite3.Database
    }).then(db => {
        const sql = `update posts set userId=${userId}, title='${title}', body='${body}' where id=${id}`;
        db.run(sql)
        .then(result => {
            console.log(result);
        })
        .then(() => {
            db.close().then(() => {
                console.log('cerrada la bd');
            });
        }).catch(error => {
            console.log('error en la consulta', error);
        });
    }).catch((error) => {
        console.log('error al abrir la bd', error);
    });
}

muestraCnPromesa(console.log);

```

## Clase usando async/await

Archivo: model.mjs
```js
import sqlite3 from 'sqlite3'
import { open } from 'sqlite'

//para depuracion
sqlite3.verbose();

const tabla='posts'
const SQL_SELECT=`SELECT * FROM ${tabla}`
const SQL_SELECT_ONE=`SELECT * FROM ${tabla} where id=?`
const SQL_INSERT=`INSERT INTO ${tabla}(userId,title,body) VALUES (?,?,?)`
const SQL_UPDATE=`UPDATE ${tabla} set userId=?, title=? ,body=? where id=?`
const SQL_DELETE=`DELETE FROM ${tabla} where id=?`

export class Posts{
    constructor(fileName){
        this.fileName=fileName
    }
    async open(){
        const db= await open({
            filename: this.fileName,
            driver: sqlite3.Database
        });
        return db
    }
    async getAll() {
        // open the database
        const db = await this.open()
        const result = await db.all(SQL_SELECT);
        db.close();
        return result
    }
    async getById(id) {
        const db = await this.open()
        const result = await db.get(SQL_SELECT_ONE,[id])
        db.close()
        return result
    }
    async run(sql, params = []) {
        console.log("recibiendo:",sql,params)
        const db = await this.open()
        const resp= await db.run(SQL_INSERT, params)
        return resp
    }
    async create(post) {
        const {userId,title,body } = post
        return this.run(SQL_INSERT,[userId,title,body])
    }
    async update(post) {
        const {userId,title,body,id } = post
        return this.run(SQL_UPDATE,[userId,title,body,id])
    }
    async delete(id) {
        return this.run(SQL_DELETE,[id])
    }
}

export default Posts
```

## Ejemplo de uso:
Archivo: controller.mjs

```js
import Posts from "./model.mjs"

const FILE_NAME="archivo.s3db"
const oposts=new Posts(FILE_NAME)

export class ControllerPosts{
    async getAll(){
        try {
            const resp=await oposts.getAll()
            return ({
                success:true,
                data:resp,
                error:null
            })
        } catch (error) {
            return ({
                success:true,
                data:[],
                error:error.message
            })
        }
    }
    async getById(id){
        try {
            const data=await oposts.getById(id)
            return ({
                success:true,
                data:data,
                error:null
            })
        } catch (error) {
            return ({
                success:true,
                data:[],
                error:error.message
            })
        }
    }
    async create(post){
        const {userId,title,body}=post
        try {
            const data=await oposts.create({userId,title,body})
            return ({
                success:true,
                data:data,
                error:null
            })
        } catch (error) {
            return ({
                success:true,
                data:[],
                error:error.message
            })
        }
    }
}
export default ControllerPosts
```

Usar la clase:
```js
import ControllerPosts from './controller.mjs'
const oCtrlPosts=new ControllerPosts()

const getAll=async ()=>{
    const data=await oCtrlPosts.getAll()
    console.log(data)
}
const getBiId=async()=>{
    const id=4
    const data=await oCtrlPosts.getById(id)
    console.log(data)
}
const insert=async (data)=>{
    const post={userId:2,title:"Titulo del post",body:"contenido del body"}
    const resp=await oCtrlPosts.create(post)
    console.log(resp)
}
```
## Refs

[Documentacion sqlite](https://www.npmjs.com/package/sqlite)

[Sqlite](https://www.npmjs.com/package/sqlite#install-sqlite)

[Sqlite](https://www.npmjs.com/package/sqlite)