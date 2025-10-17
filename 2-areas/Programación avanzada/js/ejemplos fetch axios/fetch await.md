
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
<script>
	async function fetchDatasintry(){
        const url='https://jsonplaceholder.typicode.com/posts/1'
        const response = await fetch(url);
        if (!response.ok) {
            throw new Error('Network response was not ok ' + response.statusText);
        }
        const data = await response.json();
        document.write(JSON.stringify(data));
	}
	//
    async function fetchData() {
        const url='https://jsonplaceholder.typicode.com/posts/1'
        try {
            const response = await fetch(url);
            if (!response.ok) {
                throw new Error('Network response was not ok ' + response.statusText);
            }
            const data = await response.json();
            document.write(JSON.stringify(data));
        } catch (error) {
            document.write('Error fetching data: ' + error.message);
        }
    }
    document.addEventListener('DOMContentLoaded', fetchData);
</script>
</html>
```

