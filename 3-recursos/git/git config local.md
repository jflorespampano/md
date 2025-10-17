
Cuando ya tienes una configuración global de Git y necesitas trabajar en un repositorio específico de tu empresa, puedes configurar opciones locales que tendrán prioridad sobre tus ajustes globales. Así puedes usar tu información personal para proyectos propios y la de tu empresa para el trabajo, todo en el mismo ordenador

###  Cómo configurar un repositorio para tu empresa

Estos son los pasos principales para configurar tu repositorio local con la información de tu empresa:

1. **Clona o crea el repositorio**: Si el repositorio de tu empresa ya existe en un servidor, clónalo. Si vas a empezar un proyecto nuevo, inicia el repositorio localmente.
```sh
git clone <URL_del_repositorio_de_la_empresa>
cd <nombre_del_directorio_del_repositorio>
```
2. **Configura tu identidad de forma local**: Sin usar el flag `--global`, los comandos de configuración solo afectan al repositorio actual.
```sh
git config user.name "Tu Nombre en la Empresa"
git config user.email "tu.email@empresa.com"
```
Esto es importante porque tu nombre y correo electrónico se incluyen en cada commit.

3. **Configura el repositorio remoto (si es necesario)**: Si clonaste el repositorio, configura automáticamente un remote llamado "origin". Puedes verificarlo con `git remote -v`. Si estás empezando un repositorio local y necesitas conectarlo a uno remoto, añádelo con:
```sh
git remote add origin <URL_del_repositorio_remoto>
```
4. **Verifica tu configuración**: Para confirmar que la configuración local está correctamente establecida, puedes listar todas las opciones de configuración que afectan al repositorio actual.

```sh
git config --list --local
#También puedes verificar
git config user.email
```

Git utiliza un sistema de configuración por capas, donde los valores más locales anulan a los globales.

| Nivel       | Comando    | Alcance                                               | Archivo de Configuración                | Uso Típico                                                                                                                                                                                                                           |
| ----------- | ---------- | ----------------------------------------------------- | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Sistema** | `--system` | Todos los usuarios del sistema                        | `[path]/etc/gitconfig`                  | Configuración general de la máquina (rara vez necesario modificar).                                                                                                                                                                  |
| **Global**  | `--global` | **Todos los repositorios** de tu usuario nfiguration) | `~/.gitconfig` o `~/.config/git/config` | **Tu información personal por defecto** (nombre, email, editor favorito) [](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Configurando-Git-por-primera-vez)[](https://www.w3schools.com/git/git_config.asp). |
| **Local**   | `--local`  | **Solo el repositorio actual**                        | `.git/config` (dentro del repositorio)  | **Información específica del proyecto**, como el email corporativo para el repositorio de la empresa [](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Configurando-Git-por-primera-vez).                     |

