# Teclas

<pre>
^ alt+94
| alt+124
` alt+96
\ alt+92
</pre>

# Atajos
|Atajos | acción |
|-------|--------|
|ctrl+ñ |abre terminal|
|ctrl+b | oculta/muestra ventana de archivos|
|alt+flecha abajo/arriba | - mueve linea|
|shift+alt+flecha abajo/arriba | - duplica linea|
|ctrl+' | - outdent|
|ctrl+L | - seleccionar toda la linea|
|ctrl + f/h | encuntra reemplaza|
|f12 | ir a definición|
|ctrl +/- | zoom|
|ctrl + T | encuentra una funcion clase o variable en todos los archivos|
|ctrl + P | encuentra un archivo específico en el directorio corriente|
|ctrl + } | comenta|
|tab/ctrl ' | identa/des|
|shift-alt-f | formatear texto seleccionado/todo el archivo, con linter/prottier|

## Editar varias ocurrencias: 
|Teclas                 | selección múltiple |
|-----------------------|-----------------------------------|
|alt + clic             | duplica cursor |
|seleccionar + Ctrl + D | seleccción múltiple |
|ctrl+f alt enter       | selecciona todas las ocurrencias |
|shift+Alt mientras arrastra | Selecciones discontinuas|

## Formatear contenido:
f1/Format Document

en settings, palomear linked editing  y activa edicion vinculada en html 

## edicion multiple

Selección múltiple con Alt + clic: Presiona la tecla Alt y haz clic en una línea de código. Luego, mantén presionada la tecla Alt y haz clic en otras líneas para agregarlas a la selección múltiple.


# complemento ES7 -react-js-snippets

<pre>
imp import 
imd import desestructurado
exp→	export default moduleName
exd→	export { destructuredModule } from 'module'
rafc crea una funcion para reac
nfn crea una funcion nombrada
anfn crea una funcion anonima
clg crea un console log
prom promesa
cmmb bloque de comentario
sto set timeout
fre→	arrayName.forEach(element => { }

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
fre→	arrayName.forEach(element => { }
fof→	for(let itemName of objectName { }
fin→	for(let itemName in objectName { }
anfn→	(params) => { }
nfn→	const functionName = (params) => { }
dob→	const {propName} = objectToDescruct
dar→	const [propName] = arrayToDescruct
sti→	setInterval(() => { }, intervalTime
sto→	setTimeout(() => { }, delayTime
prom→	return new Promise((resolve, reject) => { }
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