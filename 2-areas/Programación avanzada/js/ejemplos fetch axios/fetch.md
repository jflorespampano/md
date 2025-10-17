
![[axios#html para get]]

## app.js con getch
```js
    fetch('https://jsonplaceholder.typicode.com/posts/1')
    .then(response => response.json())
    .then(data => document.write(JSON.stringify(data)))
    .catch(error => document.write('Error fetching data:', error));
```

![[axios#formulario para post]]

## codigo app.js con fetch

```js
document.getElementById('postForm').addEventListener('submit', function(event) {
    event.preventDefault(); // Prevent the default form submission
    const form = document.getElementById('postForm');  
    const apiUrl = 'https://jsonplaceholder.typicode.com/posts';
    const formData = new FormData(form);
    const formDataObject = Object.fromEntries(formData.entries());
  
    fetch(apiUrl, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(formDataObject)
    })
    .then(response => response.json())
    .then(data => {
            console.log('Response:', data);
            alert('Post creado satisfactoriamente!');
    })
    .catch(error => {
            console.error('Error:', error);
            alert('un error ha ocurrido en la creación del post.');        
    });
});
```
