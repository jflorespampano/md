---
categoría: ia
tipo: conceptos
---

### Regresión frente a clasificación

Un modelo de **regresión** predice valores continuos. Por ejemplo, los modelos de regresión hacen predicciones que responden a preguntas como las siguientes:

¿Cuál es el valor de una casa en California?
¿Cuál es la probabilidad de que un usuario haga clic en este anuncio?

Un modelo de **clasificación** predice valores discretos. Por ejemplo, los modelos de clasificación hacen predicciones que responden a preguntas como las siguientes:

¿Un mensaje de correo electrónico determinado es spam o no es spam?
¿Esta imagen es de un perro, o un gato?

### Regresión lineal

#### Algunos conceptos de recta.

ecuación de la recta:

$$y=mx+b$$

  

$y$ es el valor a predecir
$m$ es la pendiente
$x$ es el valor de un atributo conocido
$b$ es la intersección en $y$

Representemos m con w1 y b con w0 :

$$y'=b+w1x1$$

es igual a

$$y'=w0+w1x1$$

Un modelo basado en 3 atributos sería:

$$y'=w0+w1x1+w2x2+w3x3$$

Gradiente es el vector de las derivadas parciales de una función de múltiples variables. El gradiente es un vector por tanto tiene dirección y magnitud.

[[Regresión logística]]

[[Ejemplo RL]]
