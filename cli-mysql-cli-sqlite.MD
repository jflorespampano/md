## sqlite

SQLite es una biblioteca en lenguaje C que implementa un motor de base de datos SQL pequeño, rápido, autónomo, de alta confiabilidad y con todas las funciones. SQLite es el motor de base de datos más utilizado en el mundo. SQLite está integrado en todos los teléfonos móviles y la mayoría de las computadoras y viene incluido en innumerables otras aplicaciones que las personas usan todos los días.

El formato de archivo SQLite es estable, multiplataforma y compatible con versiones anteriores y los desarrolladores se comprometen a mantenerlo así hasta el año 2050. Los archivos de base de datos SQLite se utilizan comúnmente como contenedores para transferir contenido enriquecido entre sistemas y como un formato de archivo a largo plazo para datos. Hay más de 1 billón (1.0e12) de bases de datos SQLite en uso activo.

El código fuente de SQLite es de dominio público y es gratuito para que todos lo usen para cualquier propósito.

**Una BD en SQlite se almacena en un unico archivo** por esto: No existe una instalación como tal de SQlite, pero si existen aplicaciones que nos pueden ayudar a crear, editar y modificar una base de datos en SQLite.

## sqlite studio

SQLiteStudio es una aplicación de escritorio para explorar y editar archivos de bases de datos SQLite. Está dirigida a personas que saben qué es SQLite o qué son las bases de datos relacionales en general.

[Manual de sQliteStudio](https://github.com/pawelsalawa/sqlitestudio/wiki/User_Manual)

## Manejadores de BD visuales para SQLite

[un db manager para sqlite](https://sqlitebrowser.org/dl/)
[**ok** un db manager para sqlite](https://sqlitestudio.pl/)
**Nota para HeidiSql** tiene un bug en el AUTOINCREMENT en el HeidiSql al usarlo con SQLite

# SQLITE Cli

CLI para Sqlite tools

El shell, viene en la herramienta sqlinetools:
sqlite-tools-win32-x86-3410000

[Descargar](https://sqlite.org/download.html)
[referencia](https://sqlite.org/cli.html)

Ejecutar el archivo: 'sqlite3.exe', cuado ejecuta este programa, si pone como primmer parametro el nombre de un archivo, si el archivo con ese nombre no existe, se crea una nueva base de datos sqlite con ese nombre, si existe se abre, si no pone nombre se crea un archivo temporal que se borra cuando salimos del programa.

* Ejecutar sqlite3

```sh
//Ejecutar sqlite 3
$ sqlite3
//cambiar directorio de trabajo
.cd c:/trabajo 
//abrir base de datos
.open provpar.s3db
mostrar tablas
.tables
////mostrar estructura de tabla
.schema partes
ejecutar senrtencia sql
select * from partes;
//muestra las base de datos abiertas
.databases
//ejecuta el codigo sql de un archivo
.read archivo.sql
salir de sqlite3
.quit
```

Ejemplo de crear tablas:
sqlite3 personas.db

```sh
#salir
.quit
#ayuda
.help
#crear tabla
create table personas(id int, nombre text);
insert into personas(1,"juan")
create table personas(
    id INTEGER PRIMARY KEY AUTOINCREMENT, 
    nombre text
);

Eejmplo crear y poblar bae de datos:
```sh
$ sqlite3 ex1
SQLite version 3.36.0 2021-06-18 18:36:39
Enter ".help" for usage hints.
sqlite> create table tbl1(one text, two int);
sqlite> insert into tbl1 values('hello!',10);
sqlite> insert into tbl1 values('goodbye', 20);
sqlite> select * from tbl1;
hello!|10
goodbye|20
sqlite>
```
```sh
//crear tabla
sqlite> CREATE TABLE tbl2 (
   ...>   f1 varchar(30) primary key,
   ...>   f2 text,
   ...>   f3 real
   ...> );
sqlite>
```

#otro ejemplo

#mostrar datos
select * from personas;

#o mostrar en columnas
.mode column
select * from personas;
```

Si entro sin nombre de archivo o con doble clic en en 'sqlite3.exe', puede cargar una base de datos así:
```sh
.open peronas.db
```

Si usted entra sin nombre de base de datos, recuerde que se crcea un archivo temporal que se borra al salir, si desea guardar el trabajo que hizo ponga:
```sh
.save nombre.db
```
Mostrar el esquema de la base de datos
```sh
.schema
#mostrar las bases de datos
.databases
```

## MySql

# Mysql CLI de Xamp

En la ventana  de Xamp en la parte superior derecha de clic en el icono de Shell, vera como respuesta:
```sh
#
```

En el Shell de Xamp para entrar a Mysql, con el usurio 'root' ponga el comando:
```sql
mysql -u root -p #responderá pidiendo un password
# contestara con la siguiente línea
Enter password:
# ponga su password o enter si no puso un password para root cuando instalo Xamp

Pruebe el siguiente comado para verificar tu conexion
SELECT VERSION(), CURRENT_DATE;

# Comandos
# ayuda de comandos
help
# mostrar las base de datos:
show databases;

# Crear base de datos
create dabase if not exists mydatabase; # la crea y la pone en uso
# Poner en uso una base de datos
use mydatabase; # la pone en uso

# Crear tablas
create table if not exists carrera (
    id int, 
    nombre varchar(50), 
    creditos int, 
    primary key(id)
);

create table if not exists alumno (
    id int not null auto_increment, 
    nombre varchar(50), 
    idcarrera int, 
    primary key(id), 
    foreign key(idcarrera) references carrera(id)
);

# Insertar datos
insert into carrera (id, nombre, creditos) values(1,”isc”,110);

# Consultar datos
select * from table;

# salir del CLI:
quit;
```

## referencias
[sqlite](https://www.sqlite.org/)
[SQLite Tools-descargar desde aquí:](https://www.sqlite.org/download.html)
[referencia CLI de sqlite: ](https://sqlite.org/cli.html)