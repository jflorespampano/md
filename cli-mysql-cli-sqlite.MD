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

Manejadores de BD visuales para SQLite
[un db manager para sqlite](https://sqlitebrowser.org/dl/)
[**ok** un db manager para sqlite](https://sqlitestudio.pl/)
**Nota** tiene un bug en el AUTOINCREMENT  el HeidiSql al usarlo con SQLite

# referencias
[descargar desde aquí:](https://www.sqlite.org/download.html)
[referencia: ](https://sqlite.org/cli.html)