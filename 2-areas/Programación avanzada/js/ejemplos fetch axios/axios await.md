
![[axios#instalar en el front end]]



![[axios#html para get]]

### app.js para get async

```js
	const url='https://jsonplaceholder.typicode.com/posts/1'
    async function get() {
        const response = await axios.get(url);
        document.write(JSON.stringify(response.data));
    }
    async function getTry() {
        try {
            const response = await axios.get(url);
            document.write(JSON.stringify(response.data));
        } catch (error) {
            document.write('Error fetching data:', error);
        }
    }
    window.onload = function() {
        get();
        getTry();
    }
```

![[axios#formulario para post]]


```js
async function postData(apiUrl, data) {
    try {
        const response = await axios.post(apiUrl, data);
        document.write(JSON.stringify(response.data));
        alert('Post created successfully!');
    } catch (error) {
        console.error('Error:', error);
        alert('An error occurred while creating the post.');
    }
}
document.getElementById('postForm').addEventListener('submit', function(event) {
    event.preventDefault(); // Prevent the default form submission
    const form = document.getElementById('postForm');  
    const apiUrl = 'https://jsonplaceholder.typicode.com/posts';
    const formData = new FormData(form);
    const formDataObject = Object.fromEntries(formData.entries());
    postData(apiUrl, formDataObject);
});
```
