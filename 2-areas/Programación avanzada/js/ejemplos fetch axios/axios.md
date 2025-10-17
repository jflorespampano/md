
## Introducción a Axios

Axios es un cliente HTTP basado en promesas para Node.js y el navegador. Es isomorfo (puede ejecutarse en el navegador y en Node.js con el mismo código base). En el servidor, utiliza el módulo http nativo de Node.js, mientras que en el cliente (navegador) utiliza XMLHttpRequest.

## instalar en el front end

```html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>

```

## Instalar en el back end

```js
npm install axios
```
## axios.get

### html para get
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
</body>
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script src="app.js"></script>
</html>
```

### Código de app.js para get

```js
document.getElementById('postForm').addEventListener('submit', function(event) {
	event.preventDefault()
    axios.get('https://jsonplaceholder.typicode.com/posts/1')
    .then(response => {
        document.write(JSON.stringify(response.data));
    })
    .catch(error => {
        document.write('Error fetching data:', error);
    });
});
```
## axios.post

### formulario para post
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Axios</title>
    <link rel="stylesheet" href="https://www.w3schools.com/w3css/5/w3.css">
  
</head>
<body>
    <div class="w3-container w3-padding-16">
        <div class="w3-container w3-blue">
            <h2>Axios POST Request Example</h2>
        </div>
        <p>LLene los campos para enviar un POST request usando Axios.</p>
        <form id="postForm" class="w3-container w3-padding-16 w3-card-4 w3-light-grey">
            <label for="userId">User ID:</label>
            <input class="w3-input" type="number" id="userId" name="userId" required>
            <label for="id">ID:</label>
            <input class="w3-input" type="number" id="id" name="id" required>
            <label for="title">Title:</label>
            <input class="w3-input" type="text" id="title" name="title" required>
            <label for="body">Body:</label>
            <textarea class="w3-input" id="body" name="body" required></textarea>
            <br>
            <button class="w3-button w3-blue" type="submit">Submit</button>  
        </form>
  
    </div>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script src="app.js"></script>
</body>
</html>
```

## Código de app.js para post

```js
document.getElementById('postForm').addEventListener('submit', function(event) {
    event.preventDefault(); // Prevent the default form submission
    const form = document.getElementById('postForm');  
    const apiUrl = 'https://jsonplaceholder.typicode.com/posts';
    const formData = new FormData(form);
    const formDataObject = Object.fromEntries(formData.entries());
  
    axios.post(apiUrl, formDataObject)
    .then(response => {
        console.log('Response:', response.data);
        alert('Post created successfully!');
    })
    .catch(error => {
        console.error('Error:', error);
        alert('An error occurred while creating the post.');
    });
});
```
## Referencias

* [Iniciando con Axios](https://axios-http.com/docs/intro)
* [Axios documentación en español](https://axios-http.com/es/docs/req_config)

