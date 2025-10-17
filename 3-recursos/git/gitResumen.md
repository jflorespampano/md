---
categoría: herramientas
tipo: bash
tags:
  - git
---

# git

[Instalar git  desde:](https://git-scm.com/downloads)

## configurar:
```sh
git --version
# configurar su nombre de usuario y mail que tiene en github
# para todos los repos de tu usuario windows
git config --global user.name "mi nombre en git hub"
git config --global user.email "miemail@mail"
# configuurar solo para el repo local
git config --local user.name "mi nombre en git hub"
git config --local user.email "miemail@mail"
# usar --local es el default pra tabto las 2 lines anteriores equivalen a:
git config user.name "mi nombre en git hub"
git config user.email "miemail@mail"

# configurar como editor predeterminaddo a VSCode
git config --global core.editor "code --wait"
# si lo desea muestre la configuración actual en el editor x defecto
git config --global -e

# mostrar configuracion
git config --list --global
git config --list --local
```


## bajar un repositorio:

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

## Clonar

Las tareas anteriores se pueden hacer con clone:

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

![[gitToken#Clonar con token | clonar con token]]

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
# -u es el equivalente corto de --set-upstream
# indica que main sigue (tracks) a `origin/main`, 
# la proxima vez solo tendras que poner pit push o git pull
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
## manejo de remotos

```sh
git remote add origin https://github.com/jflorespampano/miRepo.git
#con token
git remote add origin https://mitoken@github.com/jfloreshotmail/miRepo.git
git remote -v #muestra las url agregadas
git remote rename old-name new-name #renombra un remoto
git remote rm origin # elimina origin = la url remota de
git pull remoto #recibe actualizaciones del remoto es la combinacion de git fetch y git merge
#para enviar una rama local a un repositorio
git push origin nombre-rama
```

## Manejar el Staging area

Agregar archivos al stging
```sh
git add archivo
git add .
```
### ver diferencias

Muestra las diferencias de mi proyecto con el staging area:
```sh
git diff
git diff archivo
```
### Recuperar archivos

![[git restore]]
![[bash (Bourne Again Shell)#Editor vi]] | 