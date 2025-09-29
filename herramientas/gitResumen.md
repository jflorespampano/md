---
categoría: herramientas
tipo: bash
---

# git

## configurar:
```sh
# configurar su nombre de usuario y mail que tiene en github
git config --global user.name "mi nombre en git hub"
git config --global user.email "miemail@mail"
# configuurar ppara un solo repo
# git config --local user.name "mi nombre en git hub"
# git config --local user.email "miemail@mail"

# configurar editor
git config --global core.editor "code --wait"
# si lo desea muestre la configuración actual en el editor x defecto
git config --global -e
```


## bajar un respositorio:

```sh
#inicializar git para esta carpeta
git init
#cambiar el nombre de la rama principal a main
git branch -m main
#agregar un remoto con la direccion de su repo de github
git remote add origin https://github.com...
#bajar el proyecto
git pull origin main
# listo ha bajado el proyecto
# si el pryecto es nuestro y hacemos cambios en el
git add .
git commit -m "comentario"
# actualizamos nuestro proyecto por si hubo cambios en el repo
git pull origin main #por si hubo algun cambio en el remoto
git push origin main #cargar mis cambios al remoto
```

### modificar tu ultimo commit

Solo se recomienda si ese commit no lo has subido a remoto
```sh
git commit --amend -m "un mensaje de commit actualizado"
```

## clonar: Las tareas anteriores se pueden hacer con clone:

```sh
git clone https://github... 
# o si quiere bajar solo una rama:
git clone -b < branchname > --single-branch < remote-repo-url >
# hacer cambios
git add .
git commit -m "comentario"
# Subir a la rama
git pull origin < branchname >
git push origin < branchname >
```


## Subir nuevo repo

```sh
# inicializar proyecto
git init
# cambiar el nombre de la rama principal a main
git branch -m main
git add .
git commit -m "first commit"

git remote add origin https://github.com/jflorespampano/minuevoRepo.git
# subir el repositorio
git push -u origin main
#listo

# Subir nuevos camios de tu proyeto a tu remoto, hacer:
# agregar tus archivos al staging
git add .
# respladar
git commit -m "commit con mis cambios"
# actualizar repo
git pull #solo git pull por que arriba uso -u
# subir proyecto
git push  #solo git push por que arriba uso -u

```

```sh
#enviar proyecto a un remoto <alias yo se lo pongo>
git remote add origin remoto
git remote -v #muestra las url agregadas
git remote rm origin # elimina origin = la url remota de
git pull remoto #recibe actualizaciones del remoto es la combinacion de git fetch y git merge
#para enviar una rama local a un repositorio
git push origin nombre-rama
```

## Remotos
```sh
git remote -v #muestra los remotos actuales
git remote rm name #remueve un remoto
git remote rename old-name new-name #renombra un remoto
```

## diferencias

Muestra las diferencias de mi proyecto con el staging area:
```sh
git diff
git diff archivo
```

## Ramas

```sh
git branch #en que versión /rama te encuentras
git branch --list #muestra las ramas

git switch -c nueva rama #crea nueva rama y cambia a ella
git switch -  #alterna entre las dos ultimas ramas
git switch rama

```

## fusionar ramas

```sh
# merge fusiona tu rama con la rama master/main
# recomendacion antes:
# git checkout master 'cambiar a la rama master/main
# git fetch 'actualiza tu rama del remoto si es el caso
# ahora si estando en la rama master/main
git merge rama-a-fusuionar
# ¡listo!
# Eliminar rama
git branch -d rama # elimina una rama
# antes de cambiar de rama debes guardar los cambios de la rama actual
# basicamente hacer git add . y git commit -m "mensaje"
```


## Trabajo diario con una rama

```sh
# 1. Moverse a la rama
git checkout feature/login

# 2. Hacer cambios
# ...editar archivos...

# 3. Commitear cambios
git add .
git commit -m "mensaje"

git pull origin feature/login
# 4. Subir cambios al remoto
git push origin feature/login
```

## Snapshots

```sh
git log #muestra los snapshots existentes
git log --oneline # con menos informacion
git log --oneline --graph # con grafica
git log --pretty=oneline #version compacta
#o con información específica
git log --pretty=format:"%h - %an, %ar : %s"
#regresar a un commit especifico
git checkout id-commit
#para regresar 1 commit anterior
git checkout HEAD~1
git checkout main #volver al estado actual
```

## Revertir cambios

El comando git revert se utiliza para deshacer cambios en el historial de confirmaciones de un repositorio. Otros comandos de 'deshacer' como git checkout y git reset, mueven los punteros HEAD y rama ref a una confirmación específica. Git revert también toma una confirmación específica; sin embargo, git revert no mueve los punteros de referencia a esta confirmación. Una operación de reversión tomará la confirmación especificada, invertirá los cambios de esa confirmación y creará una nueva "reversión de confirmación". Luego, los punteros de referencia se actualizan para apuntar al nuevo compromiso de reversión, convirtiéndolo en la punta de la rama.

```sh
#mostramos commit
# mostrar comits
git log --oneline # con menos informacion
git log --oneline --graph # con grafica

git revert HEAD # revert al commit anterior

#ejemplo regresar a un commit cualquiera
git revert a1e8fb5
# si hay conflictos abrira el editor con el archivo en conflicto
# haga los cambios pertinentes en el editor
git add archivo #agregue el archivo ya corregido o eliminelo con git rm archivo
# ejecute
git revert --continue
# ponga el mensaje del commit en su editor y cierre el archivo
# ¡Listo!
# una opcion es que despues de hacer git add archivo haga:
git commit -m "mensaje del nuevo commit"
```

Otra forma de regresar

Suponga que esta trabajando y ha hecho 5 commit donde estuvo probando un código que al final no sale bien y su proyecto ha dejado de funcionar, entonces quiere regresar a una versión segura, hasta un punto antes de probar ese código que salió mal.
```sh
#mostramos instantaneas 
git log --oneline
# suponga que tiene estos snapshot
#b7119f2 continuar probando y sale mal agregar "codigo FALLO"
#872fa7e empiezo a probar un nuevo codigo agregar "codigo nuevo"
#a1e8fb5 hacer cambios importantes en hello.txt "codigo importante"
#435b61d agregando a hello.txt el texto "codigo 1"
#9773e52 creaado hello.txt con el texto "iniciando"
#suponga que quiere revertir hasta "cambios importantes" a1e8fb5
#vamos a esa instantanea
git checkout a1e8fb5
git show a1e8fb5 #muestra los datos del snpashot por se desea verlos
#Estás en el estado 'HEAD separado'. Puedes mirar alrededor, hacer cambios experimentales y hacerles commit, y puedes descartar cualquier confirmación que hagas en este estado sin afectar a ninguna rama volviendo a una rama.

# si desea hacer cambios, necesitará 
  # hacer los cambios y sacar instantanea con los cambios
  git add .
  git commit -m "mensaje"

# a continuación crear una nueva rama con los nuevos cambios
# Si quieres crear una nueva rama para conservar las confirmaciones que creas, usando -c con el comando switch. Ejemplo:
# forma 1:
 git switch -c ramanueva
# forma 2:
 git checkout -b ramanueva
# fin de forma

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

## resumen git revert

Caso básico:
```sh
# Deshacer el ÚLTIMO commit
git revert HEAD

# Se abrirá el editor para el mensaje del commit de revert
# Guarda y cierra para completar la operación

# o usar:
git revert HEAD -m "Revert: agregar funcionalidad bugueada"
```

## Deshacer commits especificos:

```sh
# Deshacer un commit por su hash
git revert a1b2c3d4

# Deshacer un rango de commits
git revert HEAD~3..HEAD
```

### ejemplo práctico git revert

```sh
# Commit accidental que agregó un archivo con error
git add archivo-con-error.js
git commit -m "feat: agregar nueva funcionalidad"
git push origin main

# ¡Oops! El archivo tiene bugs y rompe la aplicación
# Solución
# Crear un commit que deshace los cambios
git revert HEAD

# Resultado:
# - Se crea nuevo commit "Revert 'feat: agregar nueva funcionalidad'"
# - Los cambios del commit original se deshacen
# - El historial se mantiene intacto
```

## git merge/rebase

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
```
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
```sh
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
```sh
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
```sh
(1)->(2)->(3)->(4)
 \
  \->(2)->(3)->(4)->(A)->(B)
```
* guarda los commit de rama 2 (A y B)
* iguala rama main a rama 2 y pone encima
* los commit de la rama 2
* ahora se puede usar el merge  fast forward en master


## Ejemplos de subir cambios a repositorio

Si trabajas solo:
```sh
# 1. Siempre verificar estado antes
git status

# 2. Hacer pull
git pull origin main

# 3. Verificar resultado del pull
git status

# 4. Si hay conflictos, resolverlos y commitear
# 5. Si todo está clean, hacer push
git push origin main

# Recomendacion
git pull --rebase origin main
# Esto reubica tus commits encima de los remotos
# Puede evitar algunos merges automáticos
```

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
#si no, generar ssh, si no existe, haciendo lo sguiente: 
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
#copiar en el portapapeles la clave publica
#$ clip < mi_clave_ssh.pub
```

A continuación:

1. En la esquina superior derecha de cualquier página en GitHub, haga clic en la fotografía de perfil y luego en  Configuración.
2. En la sección "Acceso" de la barra lateral, haz clic en  Claves SSH y GPG.
3. Haga clic en Nueva clave SSH o en Agregar clave SSH.
4. En el campo "Title" (Título), agrega una etiqueta descriptiva para la clave nueva. Por ejemplo, si estás utilizando un portátil personal, puedes llamar a esta clave "Portátil personal".
5. Selecciona el tipo de clave, ya sea de autenticación o de firma. Para más información sobre la firma de confirmación, 6. consulta Acerca de la verificación de firma de confirmación.
7. En el campo "Clave", pega tu clave pública.
8. Haga clic en Agregar clave SSH.
9. Si se te solicita, confirma tu contraseña en GitHub. Para más información, consulta Modo sudo.

[ref](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

## etc

```sh
# comndos del editor vi
# al entrar al editor vi entra en modo comando, puede moverse con las flechas en el texto y ejecutar comanddoa para:
# editar buscar reemplazar NO puede modificar el texto en modo comando, para hacerlo debera ejecutar  el comado
# i o el comando a que lo lleva a modo edicion, para salir de modo edicion preione tecla <esc>
# comandos:  comando i o comando a. si presiona el comano x por ejemplo, borra la letra en el cursor
# con el comando i entra a modo inserción
i #insertar texto en la posicion actual - entra a modo edicion
a #insertar texto despues de la posicion actual - entra  a modo edicion
esc sale de edicion a modo comando
# En modo comando:
:wq guarda y sale del archivo
:q! sale sin guardar
```
Ejemplo de Archivo: .gitignore
```sh
# Ignorar la carpeta de dependencias
node_modules/

# Ignorar archivos de entorno
.env

# Ignorar logs
*.log
npm-debug.log*

# Ignorar cache
.cache/

# Ignorar compilados
dist/
build/

```


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
# ejemplo
touch redme.md
```