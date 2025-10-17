---
categoría: herramientas
tipo: bash
---
# Windows power shell


## crear un perfil de usuario
```sh
new-item -type file -path $profile -force
```

crea una carpeta WindowsPowerShell con un archiov .ps1 dentro que contiene la configuracion de ps

Ver el prompt actual:
```sh
(Get-Command prompt).Definition
```

funcion cambiar el promp
```sh
function prompt {
    Write-Host ("jflores>") -nonewline -foregroundcolor Yellow
    return " "
  }
```

```sh
function prompt { 
  '[jf] ' + ($pwd -split '\\')[0]+'...\'+($pwd -split '\\')[-1] + '> ' 
}
```
## Referencias

[Power shell](https://blog.victorsilva.com.uy/powershell-customizar-prompt/)
