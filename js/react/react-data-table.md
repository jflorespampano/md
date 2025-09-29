# react-data-table

Si buscas un equilibrio entre la fuerza y ​​una biblioteca de tablas sencilla pero flexible, dale una oportunidad a React Data Table Component. Si necesitas un clon de Excel, esta no es la biblioteca de tablas de React que buscas.

[react-data-table](https://www.npmjs.com/package/react-data-table-component)

La documentación contiene información sobre la instalación, el uso y las contribuciones.

[doc](https://react-data-table-component.netlify.app/?path=/docs/getting-started-intro--docs)

## instalación

```sh
npm install react-data-table-component
```
Si NO tiene instalados aún los componentes con estilo

```sh
npm install react-data-table-component styled-components
```

## ejemplos

Pruebe los ejemplos de: 
[ejemplos](https://react-data-table-component.netlify.app/?path=/docs/getting-started-examples--docs)

## ejemplo 2

Para el siguiente ejemplo, pruebe el siguiente end-point desde:

* [su navegador poniendo la ruta:] (https://gorest.co.in/public/v2/users)
* curl ejecutando el comando: curl https://gorest.co.in/public/v2/users

Como ve devuelve una lista de usuarios, usaremos esa url para crear una tabla con esa lista.

```js
import 'styled-components'
import DataTable, {createTheme} from "react-data-table-component"
import { useEffect, useState } from 'react'

const Table = () => {
  // 1 hooks
  const [users, setUsers]=useState([])
  // 2 fetch
  const URL='https://gorest.co.in/public/v2/users'
  const showData=async ()=>{
    const response=await fetch(URL)
    const data=await response.json()
    console.log(data)
    setUsers(data)
  }
  useEffect(() => {
    showData()

  }, [])
  
  // 3 cofigurar columnas
  const columns=[
    {
      name:'ID',
      selector: row=>row.id
    },
    {
      name:'NAME',
      selector: row=>row.name
    },
    {
      name:'E_MAIL',
      selector: row=>row.email
    },
  ]
  // personalizar tema
  // en: https://react-data-table-component.netlify.app/?path=/docs/api-custom-themes--docs
  createTheme('solarized', {
    text: {
      primary: '#268bd2',
      secondary: '#2aa198',
    },
    background: {
      default: '#002b36',
    },
    context: {
      background: '#cb4b16',
      text: '#FFFFFF',
    },
    divider: {
      default: '#073642',
    },
    action: {
      button: 'rgba(0,0,0,.54)',
      hover: 'rgba(0,0,0,.08)',
      disabled: 'rgba(0,0,0,.12)',
    },
  }, 'dark');
  //renderizar
  return (
    <div>
      <h1>Data table Users</h1>
      <DataTable 
        columns={columns}
        data={users}
        theme='solarized'
        pagination
      />
    </div>
  )
}
export default Table

```

pruebe nuevamente el código eliminaando la línea: 

```js
theme='solarized'
```
y la creación del tema.

[En esta liga, vea como personaizar su tema](https://react-data-table-component.netlify.app/?path=/docs/api-custom-themes--docs)
