---
categoría: herramientas
tipo: bash
tags:
  - git
---

### Cómo Manejar una Fusión con Conflicto

A veces, Git no puede combinar los cambios automáticamente porque ambas ramas modificaron la misma parte de un archivo. Así se resuelve:

1. **Git te informará del conflicto** al ejecutar `git merge`:

```sh
git merge nueva-seccion-footer
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```
2. **Usa `git status`** para ver los archivos con conflictos.
3.  **Abre el archivo en conflicto** (ej. `index.html`). Verás marcas especiales:

```sh
<div id="footer">
<<<<<<< HEAD
<p>Contacto: email@ejemplo.com</p>
=======
<p>Para contactarnos: soporte@ejemplo.com</p>
>>>>>>> nueva-seccion-footer
</div>
```

4. **Edita el archivo** para decidir el contenido final. Por ejemplo:

```html
<div id="footer">
  <p>Contacto: soporte@ejemplo.com</p>
</div>
```
5. **Finaliza la fusión**:

```sh
# Marca el archivo como resuelto
git add index.html
# Confirma la fusión
git commit -m "Resolver conflicto al fusionar nueva-seccion-footer"
```

Git creará un **nuevo commit de fusión** que une las historias de ambas ramas.

### Consejos Clave

- **Siempre confirma o guarda (stash) tus cambios** antes de cambiar de rama o fusionar para evitar problemas.
- **Verifica en qué rama estás** con `git status` antes de fusionar. Debes estar en la rama que recibirá los cambios (ej. `main`).
- **Elimina las ramas fusionadas** para mantener tu repositorio ordenado: `git branch -d nombre-de-la-rama`