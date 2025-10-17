# props

Ejemplo:

```js
import React, { useState } from 'react';

function App() {
  const [data, setData] = useState({ id: 0, nombre: "", edad: 0 });

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setData({
      ...data,
      [name]: value
    });
  };

  return (
    <div>
      <h1>Aplicación React</h1>
      <Formulario data={data} handleInputChange={handleInputChange} />
      <Tabla data={data} />
    </div>
  );
}

function Formulario({ data, handleInputChange }) {
  return (
    <div>
      <h2>Formulario</h2>
      <form>
        <label>
          ID:
          <input
            type="number"
            name="id"
            value={data.id}
            onChange={handleInputChange}
          />
        </label>
        <br />
        <label>
          Nombre:
          <input
            type="text"
            name="nombre"
            value={data.nombre}
            onChange={handleInputChange}
          />
        </label>
        <br />
        <label>
          Edad:
          <input
            type="number"
            name="edad"
            value={data.edad}
            onChange={handleInputChange}
          />
        </label>
      </form>
    </div>
  );
}

function Tabla({ data }) {
  return (
    <div>
      <h2>Tabla</h2>
      <table border="1">
        <thead>
          <tr>
            <th>ID</th>
            <th>Nombre</th>
            <th>Edad</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>{data.id}</td>
            <td>{data.nombre}</td>
            <td>{data.edad}</td>
          </tr>
        </tbody>
      </table>
    </div>
  );
}

export default App;
```