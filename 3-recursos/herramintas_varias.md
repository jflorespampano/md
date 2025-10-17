---
categoría:
tipo: etc
---
## herramientas

Replit.com es una plataforma en línea que permite programar, colaborar y alojar proyectos directamente desde el navegador, sin necesidad de instalar software localmente. Es muy popular entre estudiantes, desarrolladores y educadores por su facilidad de uso y sus características colaborativas.

[replit](https://replit.com/)
[editor/compilador de código en línea](https://codesandbox.io/s/react-hook-form-get-started-j5wxo)
[Excalidraw](https://excalidraw.com/)
[obsidian, probar](https://obsidian.md/)
[notion, probar](https://www.notion.com/es)
[validar json](https://jsonlint.com/)
[navaja suiza para desarrolladores](https://devtoys.app/)

Probar código en js

[jsplayground](https://www.jsplayground.dev/)

visualizar json en graficos interactivos

[jsoncrack](https://jsoncrack.com/)

caja de herramientas

[omatsuri](https://omatsuri.app/)

herramienta para hacer apps responsivas

[responsively](https://responsively.app/)


## css

[probar css en linea](https://codi.link/%7C%7C)
[calculador de especificidad] (https://specificity.keegan.st/)
[manz](https://lenguajecss.com/)
[web.dev aprender css](https://web.dev/learn/css?hl=es)
[css](https://developer.mozilla.org/es/docs/Web/CSS)
[z-index](https://web.dev/learn/css/z-index?hl=es)
[retors css](https://www.frontendmentor.io/)

## color piker

[color piker](https://www.w3schools.com/colors/colors_picker.asp)
[image color piker](https://imagecolorpicker.com/)
[color piker](https://rgbcolorpicker.com/)
[oklch](https://oklch.com/#70,0.1,89,100)

## pandoc

[convertidos universal](https://pandoc.org/)

Instalar pandoc:

```sh
# Instalar Pandoc: https://pandoc.org/installing.html
# convertir
pandoc archivo.md -o archivo.html --mathml
pandoc archivo.md -o archivo.pdf --pdf-engine=lualatex # si genero pdf con latex
```

## react

en el archivo: .eslint.cjs
en la entrada:
```json
rules: {
    'react/jsx-no-target-blank': 'off',
    'react-refresh/only-export-components': [
      'warn',
      { allowConstantExport: true },
    ],
    "react/prop-types":"off",
  },
```
poner la linea: "react/prop-types":"off",
para que eslint no marque advertencias por la falta de descripcion de tipos


## iconos Bootstrap

[iconos](https://icons.getbootstrap.com/?q=clos)

## imagenes svg

[gallery](https://pixels.market/)

[fotografias](https://unsplash.com/documentation)

## vscode
ctr-sift-L selecciona todas las ocurrencias del texto seleccionado
shift-alt-f formatear texto seleccionado/todo el archivo, con linter/prottier

## box-sizing

Poner border-box para que el tamaño de la caja sea el que se pone en width y height
```css
box-sizing: content-box/border-box;
```

### CSS en lugar de usar el border usar outline, para no afectar las dimenciones del elemento:

```css
  outline: 3px solid red;
```

Probar:
```css
 input:focus{
  outline:1px solid yellow;
 }
```