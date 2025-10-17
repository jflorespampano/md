---
categoría: herramientas
tipo: bash
tags:
  - git
---

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

