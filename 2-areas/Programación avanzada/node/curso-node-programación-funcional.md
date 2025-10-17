## Programación funcional

Aunque js no es un lenguaje con el paradigma funcional, podemos usar algunas herramientas del lenguaje para escribir programas en este paradigma:

Las herramientas a usar son:
1. Asegurar inmutabilidad de los datos con los que trabaja tu aplicación.
2. Usar funciones puras.
3. Uso de funciones de orden superior.  
4. Uso del currying.
5. Composición de funciones.

### inmutabilidad

Los valores de las variables deben ser inmutables, para lograr esto puede declarar constantes cuando sea posible.
También hay que recordar que las variables se asignan por valor y los objetos y arreglos se asignan por referencia.
vea objetos e inmutabilidad mas adelante.

### funciones puras 

Una función pura tiene dos propiedades esenciales:

1. El valor que retorna depende sólo de los argumentos de entrada. O lo que es lo mismo, el valor de retorno no cambiará si los valores de entrada no cambian.
2. No puede modificar nada que este fuera de su ámbito.

**Para lograr esto vea mas adelante el operdor spread**

### currificación 

Currificar consiste en convertir una función de múltiples variables en una secuencia de  funciones unarias

Esto hace que, si la función tiene N argumentos de entrada, nunca se ejecutará si no le proporcionamos todos los argumentos de entrada que pide, al contrario de lo que ocurre por defecto en JavaScript (como con parseInt, que podíamos ejecutarla con un sólo argumento a pesar de recibir dos).

```js
const suma = (a, b) => a + b;

suma(3, 5); //=> 8
suma(3)(5); //=> TypeError

//funcion currificada
const suma = (a) => (b) => a + b;
suma(3)(5); //=> 8
```
### funciones de orden superior 

Las funciones de orden superior son aquellas que reciben una o más funciones como argumento o bien devuelven funciones como resultado. Nos interesan porque nos permiten reutilizar la forma de ejecutar otras funciones. En especial nos serán muy útiles map, filter y reduce, los pilares de la programación funcional en JavaScript, su interés principal está en usarlo sobre arrays.

### composición de funciones 

```js
const original = [80, 3, 14, 22, 30];

const result = original
    .filter((value) => value%2 === 0)
    .filter((value) => value > 20)
    .reduce((accumulator, value) => accumulator + value);

console.log(result); // 132
```
en construcción [ver:](https://lemoncode.net/lemoncode-blog/2017/9/5/introduccion-programacion-funcional-javascript)
