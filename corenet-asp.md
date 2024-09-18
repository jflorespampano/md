## dotnet
NET Core es una plataforma de desarrollo de aplicaciones multiplataforma de código abierto, que permite a los desarrolladores crear aplicaciones de alta calidad para diferentes plataformas, incluyendo Windows, MacOS y Linux. Puede descargarlo desde aquí: 

[core net](https://dotnet.microsoft.com/es-es/download)


## Core net y VSCode.
### instalar extension 
Para trabajar en el editor VSCode instalar la extensión C# de Microsoft, esta pregunta por instalar el corenet si no lo ha instalado.

### construir proyecto en core net
Para ver las versiones de net instaladas:
```sh
dotnet --list-sdks
#ver sdks y runtimes instalados
dotnet --info
dotnet -h muestra ayuda sobre un comando x ejemplo
dotnet new -h
dotnet new list #muestra las plantillas istaladas
```
Para cosntrur un nuevo proyecto de consola 
En la consola:
* Crear una carpeta de proyecto
* Ir a esa carpeta `cd carpeta`
* Ejecutar para construir  en version 7.0
```sh
dotnet new console --framework net7.0
```
* Ejecutar  para construir  en version 7.0
```sh
dotnet new console -f net7.0
```
* Ejecutar  para construir  en version 5.0
```sh
dotnet new console -f net5.0
```
* Construir  proyecto
```sh
dotnet build
```
* Ejecutar proyecto 
```sh
dotnet run
```

Otra forma es ejecutar el comando:

```sh
#-o output directory
dotnet new console -o sample1
cd sample1
#ejecutar proyecto
dotnet run
#elegir lenguaje
dotnet new console --languaje "F#"/"VB"
```

```sh
dotnet new web -o nombre-de-mi-web
dotnet new webapi -o nombre-de-mi-api
```
En core net  7.0 puede escribir el código principal de la aplicación sin función main, esto se le llama instrucciones de nivel superior, vea mas sobre esto en:

[instrucciones de nivel superior](https://learn.microsoft.com/es-es/dotnet/csharp/fundamentals/program-structure/top-level-statements)


Puede crear un proyecto indicando que quiere la estructura del main en lugar de instrucciones de nivel superior, lo pude hacer así:
```sh
dotnet new console --use-program-main -o proyecto-1
```
Puede crear un proyecto para una version especifica (siempre y cuando tenga instalada esa versión):
```sh
dotnet new console -f net6.0 -o mirpoyecto
```

## generar ejecutable
```sh
# generar ejecutable
dotnet publish -c Release -r win10-x64
# publicar a un solo archivo
dotnet publish -c release -r win10-x64 -p:PublishSingleFile=true -o .\ejecutable
```

[ref](https://www.youtube.com/watch?v=f-HP8yOfGxg)
## referencias
[comados de cli](https://learn.microsoft.com/es-es/dotnet/core/tools/)

[introduccion a core net](https://learn.microsoft.com/es-es/dotnet/core/introduction)

[documentacion en español](https://learn.microsoft.com/es-es/dotnet/core/get-started)

[descargar plataforma](https://dotnet.microsoft.com/es-es/download/dotnet)

[hola mundo en core net](https://learn.microsoft.com/es-es/dotnet/core/get-started)

[mas sobre versiones de c#](https://learn.microsoft.com/es-es/dotnet/csharp/whats-new/csharp-10)

[vscode con core net 7 y c# 11](https://dev.to/jjorozcodev/visual-studio-code-con-net-7-y-c-11-gli)

[apis](https://dotnet.microsoft.com/es-es/apps/aspnet/apis)