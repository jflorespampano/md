---
categoría: herramientas
tipo: bash
tags:
  - git
---


>[!warning] Nota
>No se recomienda usarlo cuando ya se han subido commits al repositorio.
>Solo se recomienda en cambios locales
>Si ya hiciste git push mejor usa git revert

git reset` mueve la **referencia de tu branch** (main) a un commit diferente, y opcionalmente afecta tres áreas:

1. **HEAD** (tu posición actual)
2. **Staging Area** (área de preparación)
3. **Working Directory** (tu directorio de trabajo)


## Los tres modos principales

### 1. `git reset --soft`

```sh
# Ejemplo
$ git reset --soft HEAD~1
```
- **Mueve HEAD** al commit anterior
- **Mantiene** los cambios en el Staging Area
- **Mantiene** los cambios en tu Working Directory
- **Uso ideal**: Cuando quieres recombinar commits o reescribir el mensaje del último commit

### 2. `git reset --mixed` (es el predeterminado)

```sh
# Estos dos comandos son equivalentes
$ git reset HEAD~1
$ git reset --mixed HEAD~1
```

- **Mueve HEAD** al commit anterior
- **Saca** los cambios del Staging Area (los "unstaged")
- **Mantiene** los cambios en tu Working Directory
- **Uso ideal**: Cuando quieres deshacer un commit pero mantener los cambios para revisarlos


### 3. `git reset --hard`

```sh
# Ejemplo
$ git reset --hard HEAD~1
```

- **Mueve HEAD** al commit anterior
- **Saca** los cambios del Staging Area
- **Elimina** los cambios de tu Workin Directory
- **¡PELIGRO!**: Pierdes todos los cambios permanentemente
- **Uso ideal**: Cuando quieres deshacer commits locales completamente y empezar de cero

## Ejemplo
```sh
# 1. Ver el estado actual
git status
On branch main
nothing to commit, working tree clean

# 2. Ver historial completo
git log --oneline
a1b2c3d Agregué función que rompe todo
e4f5g6h Agregué validación de email  
i7j8k9l Implementación inicial del login

# 3. Hacer reset al commit bueno (e4f5g6h)
git reset --hard e4f5g6h

# 4. Verificar el nuevo estado
git log --oneline
e4f5g6h Agregué validación de email
i7j8k9l Implementación inicial del login

# 5. Verificar que el código funciona correctamente
```
Usando referencias relativas:
```sh
# Volver 1 commit atrás
$ git reset --hard HEAD~1

# Volver 2 commits atrás  
$ git reset --hard HEAD~2
```
>[!note] nota
>**hard** es destructivo: elimina permanentemente los cambios
>Solo usa `git reset --hard` en commits locales que NO hayas subido al repositorio remoto
>Si ya hiciste `git push`, mejor usa `git revert` en lugar de git reset

    
Si te equivocas con el reset puedes revertirlo:

```sh
# Ver todas las acciones recientes
git reflog

# Revertir el reset
git reset --hard <hash-del-commit-que-borraste>
```

### modificar mensaje de tu ultimo commit

Solo se recomienda si ese commit no lo has subido a remoto
```sh
git commit --amend -m "un mensaje de commit actualizado"
```
