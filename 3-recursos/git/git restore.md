---
categoría: herramientas
tipo: bash
tags:
  - git
---

### Git restore

`git restore` es un comando introducido en Git 2.23 que te permite deshacer cambios en archivos de tu directorio de trabajo o área de preparación (staging area), siendo una alternativa más moderna y especializada a comandos antiguos como `git checkout` y `git reset`El git restore es una nueva opción cuando estamos trabajando y necesitamos restaurar algún archivo o el proyecto por completo , y eso es lo que git checkout también tiene, pero el git restore es específicamente para trabajar con esta parte de restauración de archivos o proyectos en un punto anterior que llamamos de fuente de restauración(source).

```sh

git restore prueba.txt #recupera prueba.txt del ultimo commit (HEAD)
git restore . #deshacer todos los cambios 
# sacar un archivo del staging area
git restore --staged archivo.txt
#para recuperar un archivo del staging area al directorio de trabajo
git restore --staged --worktree archivo
#recuperar del historial
git restore a.txt --source f544960 #a.txt es restaurado al estado que tenía en el commit f544960
#sintaxis recomendada
git restore --source=abc123 mi_archivo.txt

# Restaurar el proyecto
#ejemplo, supanga que tiene el commit con id:c776f0cdefd3c6e05165feecbfe6d6a484436f16
#restaurar el proyecto a ese commit sería
git checkout c776f0cdefd3c6e05165feecbfe6d6a484436f16
#seria asi con git restore:
git restore --source c776f0cdefd3c6e05165feecbfe6d6a484436f16