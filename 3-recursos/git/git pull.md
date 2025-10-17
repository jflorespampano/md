---
categoría: herramientas
tipo: bash
tags:
  - git
---

### git pull 

Se usa para extraer datos desde un remoto y actualizar el repositorio local. 

`git pull origin main` realiza dos tareas:

* `git fetch origin` el cual pregunta si el remoto tiene nuevos cambios, de tenerlos los descarga a la rama oculta `remotes/origin/main`
* `git merge origin main` el cual fusiona las 2 ramas, la rama que bajo del remoto y la nuestra.
