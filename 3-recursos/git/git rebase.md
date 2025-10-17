---
categoría: herramientas
tipo: bash
tags:
  - git
---


Rebase es una de las dos utilidades de Git que se especializa en integrar cambios de una rama a otra. La otra utilidad de integración de cambios es git merge. La fusión es siempre un registro de cambios que avanza hacia adelante. Alternativamente, rebase tiene potentes funciones de reescritura del historial. 

Imagina que tu proyecto tiene dos ramas: `main` (la rama principal) y `feature` (una rama con una nueva funcionalidad). Mientras trabajabas en `feature`, la rama `main` avanzó con nuevos commits. Git rebase te permite mover toda tu rama `feature` para que comience desde la punta más reciente de `main`, como si la hubieras creado recién hoy.

- **El proceso básico**: Rebase "reubica" tus commits. Git crea commits nuevos (con identificadores diferentes) en la base deseada y mueve tu rama allí.
- **El comando estándar** se ejecuta así (tienes que estar en tu rama de trabajo, por ejemplo, `feature`):

```sh
git checkout feature
git rebase main
```
Esto reproducirá cada commit de `feature` sobre `main`.

## ejemplo Merge
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
con el comando log podemos ver que pasó:
```sh
$ git log --oneline
0f1e0fd (HEAD -> features) b en features
d273c5c a en features
fbcadc9 (master) 3 en master
3d13883 2 en master
29d0b8d 1 en master
#ahora vamos a master
$ git checkout master
#vamos a master y hacemos merge con features
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
* ahora se puede usar el merge fast forward en master


>[!note] merge fast forward
>Un **"fast forward merge"** en Git es un tipo de fusión que se produce cuando no hay nuevos commits en la rama base (como `main`) desde que se creó la rama de características. En lugar de crear un nuevo commit de fusión, Git simplemente mueve el puntero de la rama base hacia adelante, hasta el commit más reciente de la rama de características, resultando en un historial lineal y limpio
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

## Merge vs rebase

| Característica           | **Git Rebase**                                              | **Git Merge**                                                               |
| ------------------------ | ----------------------------------------------------------- | --------------------------------------------------------------------------- |
| **Historial resultante** | **Lineal y limpio**. Oculta que el trabajo fue en paralelo. | **Muestra la bifurcación**. Crea un **commit de fusión** que une las ramas. |
| **Filosofía**            | **Reescribe el historial**. Crea commits nuevos.            | **Preserva el historial** tal como sucedió. No modifica commits existentes. |
| **Uso seguro**           | **Solo en ramas locales**, antes de hacer push.             | **Siempre seguro**, incluso en ramas públicas.                              |
