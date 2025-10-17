# Lenguaje c/c++
## caracteres mas usados:
| (alt+124)

\ (alt+92)

~ (alt+126)

` (alt+96)

|| 

&&


## Compilar c++ en VsCode con gcc

Para compilar programas en c/c++ en Windows, tiene varias opciones, aquí trabajaremos con el compilador **gcc** y el editor **Visual Studio Code**.

## Instalar gcc
### Opción 1 gcc con tdm-gcc

Para instalar el compilador gcc le muestro 3 opciones:

### Opción 1 gcc con tdm
En la liga:

[descargar tdm gcc](https://jmeubank.github.io/tdm-gcc/)

Puede descargar una implementación de gcc, esta opción configura el path del sistema para acceder al compilador.

### Opción 2 gcc con Dev c++
Dev C++ no es un cimpilador es un ambiente que usa como  compilador gcc.

[Liga para descargar Dev C++ 5.11](https://sourceforge.net/projects/orwelldevcpp/)

Dev-Cpp no configura el path para acceder al compilador. Si ya instalo Dev-Cpp, en una de las carpetas de la instalación debe tener la carpeta: **MingW64** `C:\Program Files (x86)\Dev-Cpp\MinGW64`, que deberá agregar al path.

### Opción 3 gcc desde MySys

MSYS2 es una colección de herramientas y bibliotecas que le brindan un entorno fácil de usar para crear, instalar y ejecutar software nativo de Windows, usando herramientas de Linux.

Mingw-w64 es una rama proyecto avanzado de **mingw.org**, creado para admitir el compilador GCC en sistemas Windows. La rama bifurcó en 2007 para brindar soporte para 64 bits y nuevas API. Desde entonces ha ganado un uso y distribución generalizados.

[liga que explica como instalar mingw en mysys2](https://parzibyte.me/blog/2021/08/23/instalar-gcc-msys2-compilador-c-cpp/)

Puede instalar Mingw de forma independiente o con Dev-Cpp o (como en mi caso) agregarlo a la instalción de MSYS, en mi caso esta en la carpeta `C:\msys64\mingw64`,  

Cualquier camino que haya tomado tendra una carpeta `mingw64`.

## Trabajar con cpp en VsCode

VSCODE es un editor libre de Microsoft que puede trabajar con varios lenguajes, aquí lo configuramos para usar c++.

### Forma 1 VsCode con tdm gcc 

Pasos

* Instalar VsCode desde [Descargar VSCode](https://code.visualstudio.com/download)
* Instalar GCC desde TDM  (se mencionó arriba)
* Agregar las extenciones:
![puntos](ext-cpp.jpg)
* Listo

Para ejecutar programas haga clic en el icono "play" (|>) en la esquina superior derecha o presione tecla f6.

## Forma 2 Trabajar VsCode con dev-cpp o MSys2
Pasos
* Instalar VSCode desde [Descargar VSCode](https://code.visualstudio.com/download)
* Instalar GCC con Dev-cpp o con mysys64
* Instalar en el path del sistema la ruta de gcc, en mi caso:

`C:\msys64\mingw64\bin`

* En la terminal de vscode, para compilar su  programa, poner el comando:

`gcc -Wall uno.cpp -o uno`

* Para ejecutarjecutar:

`./uno`

## Forma 3 crear tarea en Vscode

En el siguiente ejemplo usaremos el gcc que instalo dev-cpp en :`C:\Program Files (x86)\Dev-Cpp\MinGW64\bin`
* en el menú terminal de vscode de clic en confifurar tareas
* ahi elija CMake:compilacion y eso crea la plantilla de compilacion
* modifique la plantilla debe verse así:

```js
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "cppbuild",
			"label": "C/C++: gcc.exe compilar archivo activo",
		
			"command": "C:\\Program Files (x86)\\Dev-Cpp\\MinGW64\\bin\\gcc.exe",
			"args": [
				"-Wall",
				"-g",
				"${file}",
				"-o",
				"${fileDirname}\\${fileBasenameNoExtension}.exe"
			],
			"options": {
				"cwd": "${fileDirname}"
			},
			"problemMatcher": [
				"$gcc"
			],
			"group": "build",
			"detail": "mi compilador de : gcc.exe"
		}
	]
}
```
Guarde el archivo.

Para ejecutar el comando, vaya a la ventana de edicion de su programa, en la iterminal de clc en la opcion: ejecutar tarea y elija la que acaba de crear.



## Referencias

[mysys](https://www.msys2.org/)
[instalar mysys](https://parzibyte.me/blog/2021/08/23/instalar-gcc-msys2-compilador-c-cpp/)
[una instroduccion a gcc](https://www.davidam.com/docu/gccintro.es.html)