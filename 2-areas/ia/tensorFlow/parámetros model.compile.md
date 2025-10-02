---
categoría: ia
tipo: tensorflow
---

```js
    // Compilar el modelo
    // optimizer: tf.train.adam() es mejor que sgd,
    // Algoritmo que ajusta los pesos del modelo para minimizar la pérdida
    // loss: 'binaryCrossentropy' es adecuado para clasificación binaria,
    // Función que mide el error del modelo
    // metrics: ['accuracy']
    // para evaluar el rendimiento del modelo durante el entrenamiento y la evaluación
    model.compile({
        optimizer: tf.train.adam(),
        loss: 'binaryCrossentropy',
        metrics: ['accuracy']
    });
```

### 1. **Optimizer: `tf.train.adam()`**

- **Qué hace**: Adam (Adaptive Moment Estimation) es un algoritmo de descenso de gradiente estocástico que adapta la tasa de aprendizaje para cada parámetro del modelo. Es eficiente y requiere poca memoria.
- **Parámetros configurables** (opcionales en `tf.train.adam()`):
    
    - **`learningRate`**: Tamaño de los pasos durante el aprendizaje (por defecto ~0.001). Valores altos aprenden rápido pero pueden pasarse del óptimo; bajos son precisos pero lentos.
        
    - **`beta1`**: Tasa de decaimiento para el primer momento (promedio de gradientes). Por defecto es 0.9.
        
    - **`beta2`**: Tasa de decaimiento para el segundo momento (promedio de cuadrados de gradientes). Por defecto es 0.999.
        
    - **`epsilon`**: Pequeña constante para estabilidad numérica (evita división por cero). Por defecto es ~1e-8.

###  2. **Loss: `'binaryCrossentropy'`**

- **Cuándo se usa**: Ideal para problemas de **clasificación binaria** donde las etiquetas son 0 o 1, y la salida del modelo es una probabilidad entre 0 y 1 .
    
- **Qué calcula**: Mide la discrepancia entre las probabilidades predichas y las etiquetas verdaderas. La función de pérdida que el modelo intenta minimizar es la suma de todas estas discrepancias

#### 3. **Metrics: `['accuracy']`**

- **Qué mide**: La **precisión** calcula la frecuencia con la que las predicciones del modelo coinciden con las etiquetas verdaderas [](https://www.tensorflow.org/api_docs/python/tf/keras/metrics/Accuracy). Es una métrica intuitiva para clasificación.
    
- **Cómo funciona**: Para `binaryCrossentropy`, esta métrica suele calcularse comparando si la probabilidad predicha (redondeada al entero más cercano) es igual a la etiqueta verdadera [](https://www.tensorflow.org/api_docs/python/tf/keras/metrics/Accuracy).


En la sentencia:

```js
model.add(tf.layers.dense({inputShape: [1], units: 1, useBias: true}));
```

El parámetro useBias: true en la capa de TensorFlow.js añade un término de sesgo al cálculo de la capa. Esto permite que el modelo aprenda patrones en los datos que no necesariamente pasan por el origen (el punto donde todos los valores de entrada son cero), lo que le otorga mayor flexibilidad y, generalmente, mejora el rendimiento. En una capa de red neuronal, el sesgo es un parámetro adicional que se agrega a la suma ponderada de las entradas antes de que se aplique la función de activación. 

- La operación que realiza una capa densa es `y = Ax + b`
    
    - `A` (the **kernel**) es la matriz de pesos que se multiplica por la entrada `x`.
        
    - `b` es el vector de sesgo que se añade al resultado..
        
    - `y` es el resultado final tras aplicar una función de activación (como 'relu' o 'sigmoid').

Qué representa: Considere el sesgo como la forma en que el modelo aprende una línea base o un desplazamiento. Sin sesgo (useBias: false), la línea y = Ax se ve obligada a pasar por el origen (0,0). Al tener sesgo, el modelo puede desplazar esta línea hacia arriba o hacia abajo para encontrar el mejor ajuste posible a los datos. Esto es crucial para la mayoría de los conjuntos de datos del mundo real, donde la relación entre la entrada y la salida rara vez es proporcional y centrada en cero.
