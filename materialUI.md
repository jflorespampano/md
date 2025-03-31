# material - Ui

Instalación
[ref](https://mui.com/material-ui/getting-started/installation/)

```sh
#
npm create vite@latest .
npm i

#
npm install @mui/material @emotion/react @emotion/styled
npm install @fontsource/roboto

```

copiar esto:
import '@fontsource/roboto/300.css';
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';

a el main.js

```js
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'

import App from './App.jsx'

import '@fontsource/roboto/300.css';
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';

import './index.css'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

instalar iconos
```sh
npm install @mui/icons-material
```

eliminar App.css
eliminar index.css y la linea: `import './index.css'` en main.js
editar App.jsx a:
```js
const App = () => {
  return (
    <div>App</div>
  )
}
export default App
```

ejemplo de boton
archivo: App.jsx
```js
import { Button } from "@mui/material"

const App = () => {
  return (
    <>
      <div>App</div>
      <Button variant="contained">mi primer btn</Button>
    </>
  )
}
export default App
```

CssBaseLine en un componente de Material ui opcional que corrige algunas incoherencias entre navegadores y dispositivos al tiempo que proporciona restablecimientos que se adaptan mejor a la interfaz de usuario de material que las hojs de estilo globales alternativas como normalize.css

Cargar CssBaseLine en main.jsx
```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'

import App from './App.jsx'

import '@fontsource/roboto/300.css';
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';
import { CssBaseline } from '@mui/material';


createRoot(document.getElementById('root')).render(
  <StrictMode>
    <CssBaseline />
    <App />
  </StrictMode>,
)
```

## container

Propiedad sx para enviar porpiedades css al control, en este ejemplo le enviamos border y boxshadow
y un pading botton (pb)
mt es margin top
Typography es una forma de mostrar estilos, permite enviar props para ajustar detalles de css, como cambiar la semantica del componente con variant
```js
import { Button, Container, Typography } from "@mui/material"

const App = () => {
  return (
    <Container sx={{
      border:2,
      boxShadow:3,
      pb:2
    }}>
      <div>App</div>
      <Typography 
        variant="h3" 
        textAlign="center"
        mt={10}
      >
        titulo</Typography>
      <Button variant="contained">mi primer btn</Button>
    </Container>
  )
}
export default App
```

Puede cambiar la semantica del componente, por ejemplo:

```js
<Typography variant="h3" component="h1">titulo</Typography>
//indicamos que tiene el estilo de un h3 pero lo renderiza como un h1 
//o puedo poner component="span" y lo renderiza como span
```

## Box

```js
import { Box, Container } from "@mui/material"

const App = () => {
  return (
    <Container sx={{
      border:2,
      boxShadow:3,
      pb:2
    }}>
      <div>App</div>
      <Box sx={{ 
        border:2 , 
        p:5,
        borderColor:"#f00",
        bgcolor:"#111",
        color:"white"}}
        component="span">Ejmplo de caja Box</Box>
    </Container>
  )
}
export default App
```

## Temas personalizar

en la lga: https://bareynol.github.io/mui-theme-creator/
puede personalizar su paleta

En el archivo main.js
```js
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'

import App from './App.jsx'

import '@fontsource/roboto/300.css';
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';
import { CssBaseline, ThemeProvider, createTheme } from '@mui/material';

const theme=createTheme({
  palette: {
    type: 'dark',
    primary: {
      main: '#3f51b5',
    },
    secondary: {
      main: '#f50057',
    },
    error: {
      main: '#c51b0f',
    },
  },
})
createRoot(document.getElementById('root')).render(
  <StrictMode>
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <App />
    </ThemeProvider>
  </StrictMode>,
)

```

## icinos

Puede bajar icons desde: https://mui.com/material-ui/material-icons/?query=ag&selected=Agriculture

en el archivo app.jsx

```js
import { Button, Container } from "@mui/material"
import AgricultureIcon from '@mui/icons-material/Agriculture';

const App = () => {
  return (
    <Container sx={{
      border:2,
      boxShadow:3,
      pb:2
    }}>
      <div>App</div>
      
      <Button 
        variant="contained" 
        color="primary"
        startIcon={<AgricultureIcon />}>mi boton</Button>
      <Button variant="contained" color="error">mi boton</Button>
      <Button variant="outlined" color="error">mi boton</Button>
      <Button variant="text" color="error">mi boton</Button>
    </Container>
  )
}
export default App
```

## material table
