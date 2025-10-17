---
categoría: herramientas
tipo: editor
---
# Teclas

<pre>
^ alt+94
| alt+124
` alt+96
\ alt+92
</pre>

# Atajos
| Atajos                        | acción                                                            |
| ----------------------------- | ----------------------------------------------------------------- |
| ctrl+ñ                        | abre terminal                                                     |
| ctrl+b                        | oculta/muestra ventana de archivos                                |
| alt+flecha abajo/arriba       | - mueve linea                                                     |
| shift+alt+flecha abajo/arriba | - duplica linea                                                   |
| ctrl+'                        | - outdent                                                         |
| ctrl+L                        | - seleccionar toda la linea                                       |
| ctrl + f/h                    | encuntra reemplaza                                                |
| f12                           | ir a definición                                                   |
| ctrl +/-                      | zoom                                                              |
| ctrl f                        | buscar                                                            |
| ctrl                          | reemplazar                                                        |
| ctrl + T                      | encuentra una funcion clase o variable en todos los archivos      |
| ctrl + P                      | encuentra un archivo específico en el directorio corriente        |
| ctrl + }                      | comenta                                                           |
| tab/ctrl '                    | identa/des                                                        |
| shift-alt-f                   | formatear texto seleccionado/todo el archivo, con linter/prottier |

Marcar plabra y ctr d duplica cursor

## Editar varias ocurrencias: 
|Teclas                 | selección múltiple |
|-----------------------|-----------------------------------|
|alt + clic             | duplica cursor |
|seleccionar palabra y Ctrl + D | seleccción múltiple |
|ctrl+shift+L       | selecciona todas las ocurrencias |
|shift+Alt mientras arrastra | Selecciones discontinuas|

## Renombrar variable:

Cambia el nombre de una variable/función en todo su ámbito.

1. Selecciona una variable y presiona F2.
2. Escribe el nuevo nombre y pulsa Enter.

ctl+f buscar

## eslint (Microsoft)

* Detección de errores en tiempo real
* Subraya errores de código mientras escribes
* Identifica problemas de sintaxis, variables no declaradas, etc.
* Impone estilo consistente (indentación, comillas, puntos y coma)
* Asegura que todo el equipo siga las mismas reglas

### Cómo se usa en VS Code:
* Instala la extensión ESLint desde el marketplace de VS Code
* Configura las reglas en un archivo .eslintrc.js o similar
* Los errores aparecen subrayados inmediatamente
* Quick fixes disponibles con clic derecho o shortcuts

## Formatear contenido:

Abrir configuracion (ctrl+,)
Editor: Default Formatter -> seleccionar foemateador
En settings, si se palomea linked editing  y activa edicion vinculada por ejemplo en html los simbolos relacionados se actualizan durante la edición.
f1/Format Document


## complemento turbo console (Anas Chakroun)

Insertar un console.log() rápidamente
* Selecciona la variable que quieres loguear.
* Presiona Ctrl + Alt + L (Windows/Linux) o Cmd + Alt + L (Mac).

Automáticamente se agregará un console.log() con la variable.
Comentar/Descomentar todos los console.log

* Ctrl + Alt + K (Windows/Linux) o Cmd + Alt + K (Mac): Comenta todos los console.log.
* Ctrl + Alt + U (Windows/Linux) o Cmd + Alt + U (Mac): Descomenta todos los console.log.

Eliminar todos los console.log
* Ctrl + Alt + D (Windows/Linux) o Cmd + Alt + D (Mac): Borra todos los console.log del archivo actual.

Loggear múltiples variables
* Selecciona varias variables (mantén Shift + clic o Ctrl + selección).
* Presiona Ctrl + Alt + L y se generarán varios console.log().

* selecciona la variable o expresión
	1. ctrl+alt+L pone un console.log
	2. alt+shift+d borra los console.log
	3. alt+shift+c comenta los los console.log
	4. alt+shift+u descomenta
	5. alt+shift+x corregir
# complemento ES7 -react-js-snippets

<pre>
imp import 
imd import desestructurado
exp	export default moduleName
exd	export { destructuredModule } from 'module'
rafc crea una funcion para reac
rfc  crea una funcion para reac
nfn crea una funcion nombrada
anfn crea una funcion anonima
clg crea un console log
prom promesa
cmmb bloque de comentario
sto set timeout
fre	arrayName.forEach(element => { })

ver snippets aqui: https://github.com/r5n-labs/vscode-react-javascript-snippets/blob/HEAD/docs/Snippets.md

Prefix	Method
imp→	import moduleName from 'module'
imn→	import 'module'
imd→	import { destructuredModule } from 'module'
ime→	import * as alias from 'module'
ima→	import { originalName as aliasName} from 'module'
exp→	export default moduleName
exd→	export { destructuredModule } from 'module'
exa→	export { originalName as aliasName} from 'module'
enf→	export const functionName = (params) => { }
edf→	export default (params) => { }
ednf→	export default function functionName(params) { }
met→	methodName = (params) => { }
fre→	arrayName.forEach(element => { })
fof→	for(let itemName of objectName { })
fin→	for(let itemName in objectName { })
anfn→	(params) => { }
nfn→	const functionName = (params) => { }
dob→	const {propName} = objectToDescruct
dar→	const [propName] = arrayToDescruct
sti→	setInterval(() => { }, intervalTime)
sto→	setTimeout(() => { }, delayTime)
prom→	return new Promise((resolve, reject) => { })
cmmb→	comment block
cp→	const { } = this.props
cs→	const { } = this.state
React
Prefix	Method
imr→	import React from 'react'
imrd→	import ReactDOM from 'react-dom'
imrc→	import React, { Component } from 'react'
imrpc→	import React, { PureComponent } from 'react'
imrm→	import React, { memo } from 'react'
imrr→	import { BrowserRouter as Router, Route, NavLink} from 'react-router-dom'
imbr→	import { BrowserRouter as Router} from 'react-router-dom'
imbrc→	import { Route, Switch, NavLink, Link } from react-router-dom'
imbrr→	import { Route } from 'react-router-dom'
imbrs→	import { Switch } from 'react-router-dom'
imbrl→	import { Link } from 'react-router-dom'
imbrnl→	import { NavLink } from 'react-router-dom'
imrs→	import React, { useState } from 'react'
imrse→	import React, { useState, useEffect } from 'react'
redux→	import { connect } from 'react-redux'
est→	this.state = { }
cdm→	componentDidMount = () => { }
scu→	shouldComponentUpdate = (nextProps, nextState) => { }
cdup→	componentDidUpdate = (prevProps, prevState) => { }
cwun→	componentWillUnmount = () => { }
gdsfp→	static getDerivedStateFromProps(nextProps, prevState) { }
gsbu→	getSnapshotBeforeUpdate = (prevProps, prevState) => { }
sst→	this.setState({ })
ssf→	this.setState((state, props) => return { })
props→	this.props.propName
state→	this.state.stateName
rcontext→	const $1 = React.createContext()
cref→	this.$1Ref = React.createRef()
fref→	const ref = React.createRef()
bnd→	this.methodName = this.methodName.bind(this)
React Native
Prefix	Method
imrn→	import { $1 } from 'react-native'
rnstyle→	const styles = StyleSheet.create({})
</pre>

## clonar repositorio

shift + ctrl +p : seleccionar git clone/ pegar direccion url/ logearse y selecciobar carpeta.

## Emet

```text
nav>ul>li*3>a[href=#]{Enlace $}
(label{Etiqueta $}+input[type="text"])*5
```

## Formatear código

```text
ctrl+k,ctrl+f # formatea bloque # no con prittier
shift+alt+f formatear todo el documento
```

```json
"editor.defaultFormatter": "esbenp.prettier-vscode"   
```