# git
1. [configuracion git](#config)
2. [bajar repositorio](#bajar_repo)
3. [clonar repositorio](#clonar_repo)
4. [subir un nuevo repositorio](#subir_repo)
5. [remotos](#remotos)
6. [comandos de linux](#comandos_linux)
7. [trabajar proyectos](#trabajar_proyectos)
8. [Ejemplo revertir cambios](#recuperar_commit)
9. [ramas](#ramas)
10. [fusionar ramas](#fusionar_rama)
11. [ramas en remoto](#ramas_remoto)
12. [referencias](#referencias)


## Intrducción
**Git** es un sistema de control de versiones distribuido muy utilizado en el desarrollo de software. Fue creado por Linus Torvalds y es conocido por su eficiencia, flexibilidad y capacidad para gestionar proyectos de cualquier tamaño.

**Github** es un portal creado para alojar el código de las aplicaciones de cualquier desarrollador, y que fue comprada por Microsoft en junio del 2018. La plataforma está creada para que los desarrolladores suban el código de sus aplicaciones y herramientas, y que como usuario no sólo puedas descargarte la aplicación, sino también entrar a su perfil para leer sobre ella o colaborar con su desarrollo.

git y github no son lo mismo, pero github utiliza git para gestionar sus proyectos. Básicamente usted lleva el control de sus versiones de proyecto con git y los respalda en la nube con github.

En estas notas usaremos la consola de git (git bash), pero tambien puede ejecutar los comando usando Power Shell (PS), para abrir una ventna de bash de clic derecho sobre la carpeta de windows donde quiera trabajar y seleccione 'git bash here'.
Praa abrir una ventanaa de Power Shell, sobre la carpeta que quiere trabajar presione a tecla 'shift' de clic derecho y seeccioen abrir PS. 

Git tiene 3 areas de trabajo:
* working directori //mi directorio de trabajo
* satagin area //archivos preparados para commit
* git directory(repositorio) //archivos respaldados (commited)

## 1 configuracion de git <a name="config"></a>

Antes de empezar a trabajar con sus proyectos, debe cofigurar git para  que este enlazado con su cuenta de github, esto lo hará solo una vez al instalar git:

```sh
# configurar su nombre de usuario y password que tiene en github
git config --global user.name "mi nombre en git hub"
git config --global user.email "miemail@mail"
#muestra la configuración actual
git config --global -e
```

## 2 bajar desde git hub <a name="bajar_repo"></a>

Si desea bajar un respositorio de github:

```sh
#arrancar (git bash o ps) 
#crear carpeta proyecto
mkdir proyecto
cd proyecto
#inicializar git para esta carpeta
git init
#cambiar el nombre de la rama principal a main
git branch -m main
#agregar un remoto con la direccion de su repo de github
git remote add origin https://github.com...
#bajar el proyecto
git pull origin main
# listo ha bajado el proyecto
# si el pryecto es nuestro y hacemos cambios en el en nuestro equipo y queremos subir los cambios al repo
# creamos un commit
git add .
git commit -m "comentario"
# actualizamos nuestro proyecto por si hubo cambios en el repo
git pull origin main #por si hubo algun cambio en el remoto
git push origin main #cargar mis cambios al remoto
```

## 3 Clonar <a name="clonar_repo"></a>

Las tareas anteriores se pueden hacer con un solo comando de la siguiente forma:

```sh
#lo anterior se puede abreviar clonando un remoto lo que deja inicializado el git y un repo del remoto ademas  crea una copia completa con todos sus commits
#descarga (clona) un proyecto desde un repositorio
git clone https://github... 

#o si quiere bajar solo una rama:
git clone -b < branchname > --single-branch < remote-repo-url >

```

## 4 subir un nuevo repositorio <a name="subir_repo"></a>

1. Creamos nuevo repositorio en GitHub (pej. minuevoRepo)
2. Creamos un nuevo proyecto en tu disco
3. Agregamos el archivo (.gitignore) para indicar los archivos/carpetas que no seran respaldados

Ejemplo de Archivo: .gitignore
```sh
node_modules
```

4. Ir a la carpeta del proyecto que deseamos subir
```sh
# ir a la carpeta del proyecto en el disco
# abriendo directamente la carpeta con Power Shell (presiona shift + clic derecho/abrir power shell)
# o abrir git bash sobre esa carpeta
# crear un arcivo README.md si no existe
echo "# nodeServerBasico" >> README.md
# inicializar proyecto
git init
git add .
git commit -m "first commit"
# cambiar nombre de rama a main
git branch -M main
# agregar el repositorio  remoto creado en github
git remote add origin https://github.com/jflorespampano/minuevoRepo.git
# subir el repositorio
git push origin main
#listo

# De hecho cuando crea un nuevo repo en github, el github le da la lista de comandos que tiene que ejecutar para subir su repo.

#para subir nuevos camios de tu proyeto a tu remoto, hacer:
git add .
git commit -m "commit con nuevos cambios"
git pull origin main #actualiza tu proyecto por si hubo cambios en el remoto hechos por otro programador de tu equipo
git push origin main #respaldar tu proyecto en el remoto

```

## 5 mas sobre remotos <a name="remotos"></a>
```sh
git remote -v #muestra los remotos actuales
git remote rm name #remueve un remoto
git remote rename old-name new-name #renombra un remoto
```

## git diff
Muestra las diferencias de mi proyecto con el staging area, es decir el area que ya guarde con `git add .`
```bs
git diff
git diff archivo
```

## 5 conamdos linux <a name="comandos_linux"></a>

Los siguientes comandos solo fucnionan en la consola bash
```sh
#muestra el path de go
echo $GOPATH
#crea archivo con lineas desde el teclado termina con ctr d
cat > archivo 
#crea archivo con ese texto
echo "# proyectoweb2" >> readme.md 
#crea un archivo vacio, si son varios se separa por espacio
touch [opciones] [nombre archivo(s)] 
#editor vi
i inserta
esc sale de edicion
:wq guarda y sale del archivo
```

## 6 trabajar con proyectos <a name="trabajar_proyectos"></a>

```sh
git init #inicializa el proyecto en rama master
git status #muestra estado del la rama actual
git add archivo #agrega archivo al staging area
git add . #agrega todos los archivos pendientes al staging
git add -A #agrega tods los archivos pendientes
git restore archivo #regresa archivo desde el staging area("elimina cambios")
git diff archivo #muestra diferencias entre en del staging area y el actual
git commit -m "mensaje"  #crea snapshot del proyecto (una versión)
git log #muestra los snapshots existentes
git log --oneline # con menos informacion
git log --oneline --graph# con grafica
git log --pretty=oneline #version compacta
#o con información específica
git log --pretty=format:"%h - %an, %ar : %s"
#regresar a un commit especifico
git checkout id-commit
#para regresar 1 commit anterior
git checkout HEAD~1
git checkout main #volver al estado actual
```

### 7 Ejemplo revertir cambios <a name="recuperar_commit"></a>

### Recuperar un solo archivo a una veriosn anterior
```sh
git log --oneline
#suponga que el id de la version a la que quiere volver es 55df4c2
git checkout 55df4c2 prueba.txt #recupera esa version del archivo
git checkout -- NOMBRE-DEL-ARCHIVO #revertirá el archivo a la versión en HEAD
```
Una opcion mejor que la anterior es usar el nuevo comando git restore.

### Git restore
El git restore es una nueva opción cuando estamos trabajando y necesitamos restaurar algún archivo o el proyecto por completo , y eso es lo que git checkout también tiene, pero el git restore es especificamente para trabajar con esta parte de restauración de archivos o proyectos en un punto anterior que llamamos de fuente de restauración(source).

```sh

git restore prueba.txt #recupera del ultimo commit
git restore . #deshacer toidos los cambios 
#para recuperar del staging area
git restore --staged archivo
#recuperar del historial
git restore a.txt --source f544960 #a.txt es restaurado al estado que tenía en el commit f544960
#ejemplo, supanga que tiene el commit con id:c776f0cdefd3c6e05165feecbfe6d6a484436f16
#restaurar el proyecto a ese commit sería
git checkout c776f0cdefd3c6e05165feecbfe6d6a484436f16
#seria asi con git restore:
git restore --source c776f0cdefd3c6e05165feecbfe6d6a484436f16
```
### Recuperar todo
Primera forma de regrasar a una version anterior:
Si lo que se desea es eliminar permanentemente los cambios realizado después de un commit  específico, el comando a usar es:
```sh
git reset --hard id-del-snapshot # por ejempo: git reset --hard 55df4c2
#o deshacer solo el ultimo cambio
git reset —-hard HEAD~
```
**Nota** No deberías utilizar nunca git reset si cualquier instantánea posterior a se ha enviado a un repositorio público. Después de publicar una confirmación, tienes que dar por sentado que el resto de los desarrolladores dependen de ella.



### Otra forma de regresar
Suponga que esta trabajando y ha hecho 5 commit donde estuvo probando un código que al final no sale bien y su proyecto ha dejado de funcionar, entonces quiere regresar a una versión segura, hasta un punto antes de probar ese código que salió mal.
```sh
#mostramos instantaneas 
git log --oneline
# suponga que tiene estos snapshot
#b7119f2 continuar probando y sale mal
#872fa7e empiezo a probar un nuevo codigo
#a1e8fb5 hacer cambios importantes en hello.txt
#435b61d creando hello.txt
#9773e52 iniciando
# suponga que quiere revertir hasta a1e8fb5
#vamos a esa instantanea
git checkout a1e8fb5
git show a1e8fb5 #muestra los datos del snpashot por se desea verlos
# si desea hacer cambios, necesitará 
# hacer los cambios y sacar instantanea con los cambios
git add .
git commit -m "mensaje"
# a continuación crear una nueva rama con los nuevos cambios
# o si no quiere hacer cambios solo recuperar lo que tenia en esa instantanea
# crea la nueva rama sin hacer cambios ni el add . ni el commit anterior
# crea la nueva rama
git checkout -b ramanueva
#para volver al estado actual
git checkout main
#tal vez quiera eliminar la rama main y quedarse con la nueva
git checkout ramanueva
git branch -D main # elimina rama main
#si pone el comando git branch -d main, y manda el mensaje de que la rama main no se ha unido (merge)
#pero como se supone que quiere eliminarla por que hay algo mal en ella
#con -D fuerza la eliminación
#finalmente cambiar el nombre de la rama nueva a main
git branch -m main

```

### git revert

El comando git revert se utiliza para deshacer cambios en el historial de confirmaciones de un repositorio. Otros comandos de 'deshacer' como git checkout y git reset, mueven los punteros HEAD y rama ref a una confirmación específica. Git revert también toma una confirmación específica; sin embargo, git revert no mueve los punteros de referencia a esta confirmación. Una operación de reversión tomará la confirmación especificada, invertirá los cambios de esa confirmación y creará una nueva "reversión de confirmación". Luego, los punteros de referencia se actualizan para apuntar al nuevo compromiso de reversión, convirtiéndolo en la punta de la rama.

`git revert HEAD~2 # esto nos pondrá en un editor de texto en donde podemos modificar el mensaje del commit.`

## 8 Ramas <a name="ramas"></a>
```sh
git branch #en que versión /rama te encuentras
git branch --list #muestra las ramas
git checkout -b nueva rama #crea una nueva rama y cambia a ella
git switch -  #alterna entre las dos ultimas ramas
git checkout rama  # cambia a esa rama
git branch -m new-name #crea nueva rama
```

## 9 fusionar rama <a name="fusionar_rama"></a>
```sh
# merge fusiona tu rama con la rama master
# recomendacion antes:
# git checkout master 'cambiar a la rama master
# git fetch 'actualiza tu rama del remoto si es el caso
# ahora si
git merge rama-a-fusuionar

git branch -d rama # elimina una rama
# antes de cambiar de rama debes guardar los cambios de la rama actual
# basicamente hacer git add . y git commit -m "mensaje"
```
### deshacer cambios en una rama
Este se hace solo si no has subido al remoto
```sh
#primero 
git log --oneline   #esto da la rama con su id
git revert id #esto deshace el commit
```

## 10 trabajar con ramas en remoto <a name="ramas_remoto"></a>
```sh
#enviar proyecto a un remoto <alias yo se lo pongo>
git remote add origin remoto
git remote -v #muestra las url agregadas
git remote rm origin # elimina origin = la url remota de
git pull remoto #recibe actualizaciones del remoto es la combinacion de git fetch y git merge
#para enviar una rama local a un repositorio
git push origin nombre-rama
```

# avanzado

```sh
git branch --all #muestra todas las ramas incluso las ocultas(las de los remotos)

```
### git pull 
Se usa para extraer datos desde un remoto y actualizar el repositorio local. 

`git pull origin main` realiaza dos tareas:

* `git fetch origin` el cual pregunta si el remoto tiene nuevos cambios, de tenerlos los descarga a la rama oculta `remotes/origin/main`

* `git merge origin main` el cual fusiona las 2 ramas, la rama que bajo del remoto y la nuestra.

### get merge/rebase
Rebase es una de las dos utilidades de Git que se especializa en integrar cambios de una rama a otra. La otra utilidad de integración de cambios es git merge. La fusión es siempre un registro de cambios que avanza hacia adelante. Alternativamente, rebase tiene potentes funciones de reescritura del historial. 

Merge
Suponga rama master y features
```
(1)->(2)->(3)
 \
  \->(A)->(B)
```
Si hacemos un merge en master con features
```sh
(master)$ git merge features
````
combina los commit de rama features y hace un commit nuevo a la rama master

`(1)->(2)->(3)->(A/B)`

```sh
#comandos
(master)$ git merge features
#Merge made by the 'ort' strategy.
# a.txt | 1 +
# b.txt | 1 +
# 2 files changed, 2 insertions(+)
# create mode 100644 a.txt
# create mode 100644 b.txt
```
Veamos ahora como quedo la rama master
```sh
(master)$ git log --oneline --graph
```
```
*   ceb81fe (HEAD -> master) Merge branch 'features' el merge
|\
| * 819db54 (features) b en fetures
| * c6ee4bd a en fetures
* | 0bf6f9d 3 en master
* | 05f10b9 2 en master
|/
* 4cdd05d 1 en master
```
### git rebase
nuevamente suponga rama master y features
```
(1)->(2)->(3)
 \
  \->(A)->(B)
```
Ejecutemos
```sh
(features)$ git revase master
```
#con el comando log podemos ver que pasó:
```sh
$ git log --oneline
0f1e0fd (HEAD -> features) b en features
d273c5c a en features
fbcadc9 (master) 3 en master
3d13883 2 en master
29d0b8d 1 en master
#ahora vamos a master
$ git checkout master
#y bamos a master y hacemos merge con features
$ git merge features
Updating fbcadc9..0f1e0fd
Fast-forward
 a.txt | 1 +
 b.txt | 1 +
 2 files changed, 2 insertions(+)
 create mode 100644 a.txt
 create mode 100644 b.txt
#ahora veamos como quedo master
$ git log --oneline --graph
* 0f1e0fd (HEAD -> master, features) b en features
* d273c5c a en features
* fbcadc9 3 en master
* 3d13883 2 en master
* 29d0b8d 1 en master
```
hizo un merge fast forward

**Resumen rebase**
```
(1)->(2)->(3)->(4)
 \
  \->(2)->(3)->(4)->(A)->(B)
```
* guarda los commit de rama 2 (A y B)
* iguala rama main a rama 2 y pone encima
* los commit de la rama 2
* ahora se puede usar el merge  fast forward en master


## 11 referencias <a name="referencias"></a>

[editar archivos md](https://rurickdev.medium.com/qué-es-markdown-o-cómo-estilizar-el-readme-de-tus-repositorios-c48af9ce7f2a)

[git commit](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Ver-el-Historial-de-Confirmaciones)

[deshaciendo cambios](https://www.atlassian.com/es/git/tutorials/undoing-changes)

[claves ssh en GitHub](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

[repositorios](https://www.atlassian.com/es/git/tutorials/syncing)

[git reset](https://www.atlassian.com/es/git/tutorials/undoing-changes/git-reset)

[manual de referencia](https://git-scm.com/docs)

[Instalar git:](https://www.youtube.com/watch?v=RAN58Qjf5uY)
[crear cuenta y configurar:](https://www.youtube.com/watch?v=LzVfVs5n3Gw&t=40s)

[git push:](https://www.youtube.com/watch?v=osO_eYMIKxM)
[git clone, git pull:](https://www.youtube.com/watch?v=IWnW0svZ9JQ&t=79s)

[ramas](basico:https://www.youtube.com/watch?v=gjKKtQVVCZU)
[diff, merge:](https://www.youtube.com/watch?v=W8rwULnu9nA)

# Etcétera
## texto por revisar y comprobar

### modificar tu ultimo commit
Solo se recomienda si ese commit no lo has subido a remoto
`git commit --amend -m "un mensaje de commit actualizado"`

## Generar tu clave publica ssh

Existen diferentes opciones para conectarse de forma remota y segura a un servidor según el sistema operativo que utilicemos. En el caso de Linux, el protocolo SSH es el más utilizado. Veremos sobre la configuración de claves SSH para mejorar aún más la seguridad al conectarnos a nuestros servidores. 

El protocolo SSH proporciona un método seguro para acceder a un recurso privado, mediante el uso de un usuario y una contraseña, de forma remota. Sin embargo, este sistema tiene un problema: la contraseña podría ser capturada por cualquier atacante, lo que pondría en riesgo la información que tengamos guardada en su interior. De ahí la importancia de usar un sistema de autenticación adicional: las claves SSH. Estas, al contrario que las contraseñas, son casi imposibles de descifrar.
La autenticación con clave pública es un método de seguridad alternativo a las contraseñas, mucho más difícil de hackear y, por lo tanto, más seguro. Este método de autenticación es recomendable usarlo para acceder tanto a servidores cloud como bare-metal.

La clave SSH consiste en la generación de un par de claves que proporcionan dos largas cadenas de caracteres —una pública y una privada—. La clave pública se instala en cualquier servidor y luego se desbloquea mediante la conexión con un cliente SSH que hace uso de la clave privada. Si las dos claves coinciden, el servidor SSH permite el acceso sin necesidad de utilizar una contraseña. No obstante, para añadir una capa de seguridad adicional, siempre podemos aumentar la protección de la clave privada usando una contraseña.

En la criptografía de clave pública, existen varios algoritmos de criptografia para generar la clave publica: (ed25519, flamel 4096, ...).

En la criptografía de clave pública, el sistema criptográfico RSA es el algoritmo basado en la factorización de números enteros más utilizado, tanto para cifrar como para firmar digitalmente. RSA es el acrónimo de Rivest, Shamir and Adleman, los apellidos de los creadores del algoritmo —Ron Rivest, Adi Shamir y Leonard Adleman—.

```sh
#crear clave ssh
#verifica si tienes clave ssh
#busca tu ruta HOME
echo $HOME
#si ahi hay una carpeta .ssh, ahi esta tu clave ssh
#si no, generar ssh, si no existe: 
#crear carpeta
mkdir $HOME/.ssh
#para crear los archivos de ssh ejecuta el comando:
ssh-keygen -t rsa -b 4096 -C "jflorespampano@gmail.com"
#pide archivo: mi_clave_ssh
#pide contrseña: contraseña : 1234
#o dejar en blanco la contraseña
#copiar clave desde el bash
#ir a carpeta en bash
#cd $HOME
#$ clip < mi_clave_ssh.pub
```




git commit -am manda los cambios al staging y hace el commit solo de los archivos seguidos