# Usar SQlite

## Crear una base de datos en SQLite

```js
const sqlite3 = require('sqlite3').verbose();
// const db = new sqlite3.Database(':memory:');
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

        db.each("SELECT * FROM posts;", (err, row) => {
            console.log(row.id + ": " + row.title);
        });
    });

    //db.close();

}

db = new sqlite3.Database('posts.sqlite3', (err) => {
    if (err) {
        console.log('Could not connect to database', err)
    } else {
        console.log('Connected to database');
    }
});
crearTabla(db);
db.close();
```

## Getionar datos de una base de datos

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