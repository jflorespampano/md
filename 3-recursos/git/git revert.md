---
categoría: herramientas
tipo: bash
tags:
  - git
---

### git revert

El comando git revert se utiliza para deshacer cambios en el historial de confirmaciones (commits) de un repositorio. A diferencia de otros comandos como `git reset` que pueden borrar el historial, `git revert` es una operación segura porque no reescribe el historial del repositorio. En su lugar, **agrega una nueva confirmación**. Esto es fundamental para mantener la integridad del historial cuando se trabaja en ramas compartidas. 

## Revertir último commit


Ejemplos de revert

```sh
# revertir el ultimo commit
git revert HEAD
# o usar:
git revert HEAD -m "Revert: mensaje"
#revertir sin editar mensaje
git revert HEAD --no-edit

# Deshacer un commit por su hash
git revert a1b2c3d4
# Deshacer un rango de commits
git revert HEAD~3..HEAD
```

>[!Note] Nota
>El comando `git revert a1b2c3d4` **deshace los cambios introducidos por ese commit específico** (`a1b2c3d4`), no regresa tu repositorio al estado de ese commit. Es una operación de "deshacer" segura que crea un nuevo commit que invierte los cambios del commit objetivo.

## Revertir a un commit en particular
```sh
#mostramos commit
# mostrar comits
git log --oneline # con menos informacion
git log --oneline --graph # con grafica

#ejemplo regresar a un commit cualquiera
git revert a1e8fb5
# si hay conflictos abrira el editor con el archivo en conflicto
# haga los cambios pertinentes en el editor guarde y cierre
git add archivo #agregue el archivo ya corregido o eliminelo con git rm archivo
# ejecute
git revert --continue
# ponga el mensaje del commit en su editor y cierre el archivo
# ¡Listo!
# una opcion es que despues de hacer git add archivo haga:
git commit -m "mensaje del nuevo commit"
```


## Ejemplo práctico revertir cambios

Tenemos una situación común: hacer varios commits y luego descubrir que uno de ellos (en el medio) introdujo un error.

```sh
# 1. Crear un nuevo directorio y repositorio para el ejemplo
mkdir ejemplo_revert
cd ejemplo_revert
git init

# 2. Crear el primer archivo y hacer un commit
echo "Contenido inicial" > archivo1.txt
git add archivo1.txt
git commit -m "Commit 1: Agrega archivo1"

# 3. Crear un segundo archivo (este será el commit problemático)
echo "Contenido correcto" > archivo2.txt
git add archivo2.txt
git commit -m "Commit 2: Agrega archivo2"

# 4. Modificar el primer archivo para un commit posterior
echo "Una línea más de contenido" >> archivo1.txt
git add archivo1.txt
git commit -m "Commit 3: Modifica archivo1"
```

Ahora tu historial tiene tres commits. Imagina que "Commit 2" agregó un archivo con un error.

### Revertir el Commit Problemático

Para deshacer los cambios del "Commit 2" (el segundo commit), usa `git revert` apuntando a él. Primero, encuentra su identificador (hash) con `git log --oneline`:

```sh
git log --oneline
# Verás una salida similar a esta:
# a1b2c3d (HEAD -> main) Commit 3: Modifica archivo1
# e4f5g6h Commit 2: Agrega archivo2
# k7l8m9n Commit 1: Agrega archivo1
```

Ahora, revierte el commit `e4f5g6h`:

```sh
git revert e4f5g6h
```

Este comando creará un **nuevo commit** que elimina el `archivo2.txt`, deshaciendo los cambios, Git abrirá tu editor para que edites el mensaje de confirmación; puedes guardar y salir para aceptar el mensaje por defecto.

### Verificar el Resultado

Tras completar el revert, verifica el estado:

```sh
ls
# archivo1.txt  (archivo2.txt ha desaparecido)
git log --oneline --graph
# o1p2q3r (HEAD -> main) Revert "Commit 2: Agrega archivo2"
# a1b2c3d Commit 3: Modifica archivo1
# e4f5g6h Commit 2: Agrega archivo2
# k7l8m9n Commit 1: Agrega archivo1
```

El `archivo2.txt` ha sido eliminado de tu directorio de trabajo, y el historial muestra el nuevo commit de reversión sin borrar el commit original.

### Opciones Útiles de Git Revert

Puedes modificar el comportamiento del comando con estas opciones

| Opción               | Descripción                                                                               | Comando de ejemplo             |
| -------------------- | ----------------------------------------------------------------------------------------- | ------------------------------ |
| `--no-edit`          | Realiza la reversión **sin abrir el editor** para el mensaje.                             | `git revert e4f5g6h --no-edit` |
| `-n` / `--no-commit` | Aplica los cambios en tu área de preparación, pero **no crea el commit** automáticamente. | `git revert e4f5g6h -n`        |

El uso de `git revert` es la opción segura para corregir errores en commits ya publicados, ya que evita reescribir el historial que otras personas podrían estar usando.

## Regresar a una versión anterior

Recuerde que revert no regresa a una versión anterior, deshace los cambios introducidos por ese commit específico. Si desea regresar a una versión anterior puede hacer lo siguiente:

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

# a continuación debe crear una nueva rama con los nuevos cambios
# forma 1:
 git switch -c ramanueva
# forma 2:
 git checkout -b ramanueva
# fin de forma


#tal vez quiera eliminar la rama main y quedarse con la nueva
git branch -D main # elimina rama main
#si pone el comando git branch -d main, y manda el mensaje de que la rama main no se ha unido (merge)
#pero como se supone que quiere eliminarla por que hay algo mal en ella
#con -D fuerza la eliminación
#finalmente cambiar el nombre de la rama nueva a main
git branch -m main

```
