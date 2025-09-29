## instalar

```sh
# verificar si esta instalado tensorflow
pip list | grep tensorflow

# Instalación estándar
pip install tensorflow
```

## tensores

Ejemplo tensores:

```python
# prueba.py
# evitar mensajes iniciales de TensorFlow
import os
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'  # 0: todos, 1: info, 2: warnings, 3: errores

# cargar biblioteca
import tensorflow as tf

# Crear tensores
scalar = tf.constant(5)                    # 0-D tensor (escalar)
vector = tf.constant([1, 2, 3])            # 1-D tensor (vector)
matrix = tf.constant([[1, 2], [3, 4]])     # 2-D tensor (matriz)

print("Scalar:", scalar.numpy())
print("Shape:", matrix.shape)
print("Data type:", matrix.dtype)
```

## ejemplo iris

Vamos a aplicar TensorFlow al conjunto de datos Iris. El objetivo es clasificar las flores en una de las tres especies (setosa, versicolor, virginica) basándose en cuatro características: longitud y ancho del sépalo, longitud y ancho del pétalo.

Pasos que seguiremos:

1. Cargar el conjunto de datos Iris.
2. Preprocesar los datos (normalizar, dividir en entrenamiento y prueba, etc.).
3. Construir un modelo de red neuronal usando TensorFlow/Keras.
4. Compilar y entrenar el modelo.
5. Evaluar el modelo y hacer predicciones.

Vamos a utilizar tf.keras para construir el modelo.

### Paso 1: cargar modelo y dataset

```python
import tensorflow as tf
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.metrics import classification_report, confusion_matrix

print("TensorFlow version:", tf.__version__)

# Cargar dataset Iris
iris = load_iris()
X = iris.data  # Características: [sepal_length, sepal_width, petal_length, petal_width]
y = iris.target  # Etiquetas: 0=setosa, 1=versicolor, 2=virginica
feature_names = iris.feature_names
target_names = iris.target_names

print("Forma de los datos:", X.shape)
print("Características:", feature_names)
print("Especies:", target_names)
print("\nPrimeras 5 filas:")
print(pd.DataFrame(X, columns=feature_names).head())
```

### Paso 2: preprocesamiento de datos

```python
# Dividir en entrenamiento y prueba
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# Escalar características (importante para redes neuronales)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

print(f"Entrenamiento: {X_train_scaled.shape}")
print(f"Prueba: {X_test_scaled.shape}")
print(f"Distribución de clases en entrenamiento: {np.bincount(y_train)}")
print(f"Distribución de clases en prueba: {np.bincount(y_test)}")
```

### Paso 3: red neuronal básica

```python
def crear_modelo_basico():
    model = tf.keras.Sequential([
        tf.keras.layers.Dense(64, activation='relu', input_shape=(4,)),
        tf.keras.layers.Dropout(0.3),
        tf.keras.layers.Dense(32, activation='relu'),
        tf.keras.layers.Dropout(0.3),
        tf.keras.layers.Dense(3, activation='softmax')  # 3 clases de salida
    ])

    model.compile(
        optimizer='adam',
        loss='sparse_categorical_crossentropy',  # Para etiquetas enteras
        metrics=['accuracy']
    )

    return model

modelo_basico = crear_modelo_basico()
modelo_basico.summary()
```

### Paso 3-a: red neuronal mas compleja

```python
def crear_modelo_avanzado():
    model = tf.keras.Sequential([
        tf.keras.layers.Dense(128, activation='relu', input_shape=(4,)),
        tf.keras.layers.BatchNormalization(),
        tf.keras.layers.Dropout(0.4),

        tf.keras.layers.Dense(64, activation='relu'),
        tf.keras.layers.BatchNormalization(),
        tf.keras.layers.Dropout(0.3),

        tf.keras.layers.Dense(32, activation='relu'),
        tf.keras.layers.Dropout(0.2),

        tf.keras.layers.Dense(3, activation='softmax')
    ])

    model.compile(
        optimizer=tf.keras.optimizers.Adam(learning_rate=0.001),
        loss='sparse_categorical_crossentropy',
        metrics=['accuracy']
    )

    return model

modelo_avanzado = crear_modelo_avanzado()
```

### Paso 4: entrenar el modelo

```python
# Callbacks para mejorar el entrenamiento
early_stopping = tf.keras.callbacks.EarlyStopping(
    monitor='val_loss', patience=20, restore_best_weights=True
)

reduce_lr = tf.keras.callbacks.ReduceLROnPlateau(
    monitor='val_loss', factor=0.5, patience=10, min_lr=0.0001
)

# Entrenar el modelo
print("Iniciando entrenamiento...")
history = modelo_avanzado.fit(
    X_train_scaled, y_train,
    epochs=200,
    batch_size=16,
    validation_data=(X_test_scaled, y_test),
    callbacks=[early_stopping, reduce_lr],
    verbose=1
)

print("✅ Entrenamiento completado!")
```

### paso 5-1: evaluar el modelo

```python
# Evaluar el modelo
test_loss, test_accuracy = modelo_avanzado.evaluate(X_test_scaled, y_test, verbose=0)
print(f"Precisión en prueba: {test_accuracy:.4f}")
print(f"Pérdida en prueba: {test_loss:.4f}")

# Gráficas de entrenamiento
def plot_training_history(history):
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 5))

    # Precisión
    ax1.plot(history.history['accuracy'], label='Precisión entrenamiento')
    ax1.plot(history.history['val_accuracy'], label='Precisión validación')
    ax1.set_title('Precisión del modelo')
    ax1.set_xlabel('Época')
    ax1.set_ylabel('Precisión')
    ax1.legend()
    ax1.grid(True)

    # Pérdida
    ax2.plot(history.history['loss'], label='Pérdida entrenamiento')
    ax2.plot(history.history['val_loss'], label='Pérdida validación')
    ax2.set_title('Pérdida del modelo')
    ax2.set_xlabel('Época')
    ax2.set_ylabel('Pérdida')
    ax2.legend()
    ax2.grid(True)

    plt.tight_layout()
    plt.show()

plot_training_history(history)
```

### Paso 5-2: hacer predicciones

```python
# Hacer predicciones
y_pred_proba = modelo_avanzado.predict(X_test_scaled)
y_pred = np.argmax(y_pred_proba, axis=1)

# Reporte de clasificación
print("Reporte de clasificación:")
print(classification_report(y_test, y_pred, target_names=target_names))

# Matriz de confusión
def plot_confusion_matrix(y_true, y_pred, class_names):
    cm = confusion_matrix(y_true, y_pred)
    plt.figure(figsize=(8, 6))
    sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', 
                xticklabels=class_names, yticklabels=class_names)
    plt.title('Matriz de Confusión - Iris Dataset')
    plt.ylabel('Etiqueta Real')
    plt.xlabel('Etiqueta Predicha')
    plt.show()

plot_confusion_matrix(y_test, y_pred, target_names)

# Probabilidades de predicción
print("\nProbabilidades de predicción (primeras 5 muestras):")
for i in range(5):
    print(f"Muestra {i+1}: {y_pred_proba[i]} → Predicción: {target_names[y_pred[i]]}")
```

## Detalles de código

### StandardScaler

La línea de código: 

$$scaler = StandardScaler()$$

crea una instancia del objeto  **StandardScaler** de la biblioteca **scikit-learn**.

Explicación detallada:

El StandardScaler es una clase que se utiliza para estandarizar las características de un dataset. La estandarización es un proceso común en el preprocesamiento de datos que transforma los datos de tal manera que tengan una media de 0 y una desviación estándar de 1.

¿Por qué se hace esto?

Muchos algoritmos de machine learning, especialmente aquellos que se basan en distancias (como SVM, KNN) o que utilizan descenso de gradiente (como redes neuronales), funcionan mejor cuando las características están en la misma escala.

Al estandarizar, evitamos que características con magnitudes grandes dominen el modelo.

### Funcionamiento

Para cada característica (columna) en el dataset, calcula:

* La media (μ) de la característica.

* La desviación estándar (σ) de la característica.

Luego, transforma cada valor x de la característica a:

```text
z = (x - μ) / σ
```

### Uso típico:

1. Se crea el escalador: 

$$scaler = StandardScaler()$$

2. Se ajusta (calcula μ y σ) con los datos de entrenamiento:

$$scaler.fit(X_train)$$

3. Se transforman tanto los datos de entrenamiento como los de prueba: 

$$X_train_scaled = scaler.transform(X_train) y X_test_scaled = scaler.transform(X_test)$$



**Nota** : Es importante ajustar el escalador solo con los datos de entrenamiento para evitar fugas de información (data leakage) desde el conjunto de prueba.



Ejemplo:

```python
from sklearn.preprocessing import StandardScaler
import numpy as np

# Datos de ejemplo
X_train = np.array([[1, 2], [3, 4], [5, 6]])
X_test = np.array([[7, 8]])

# Crear y ajustar el escalador
scaler = StandardScaler()
scaler.fit(X_train)

# Transformar los datos
X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)

print("Media de cada característica en entrenamiento:", scaler.mean_)
print("Desviación estándar de cada característica:", np.sqrt(scaler.var_))
print("Datos de entrenamiento escalados:\n", X_train_scaled)
print("Datos de prueba escalados:", X_test_scaled)
```

Salida:

```text
Media de cada característica en entrenamiento: [3. 4.]
Desviación estándar de cada característica: [1.63299316 1.63299316]
Datos de entrenamiento escalados:
 [[-1.22474487 -1.22474487]
 [ 0.          0.        ]
 [ 1.22474487  1.22474487]]
Datos de prueba escalados: [[2.44948974 2.44948974]]
```

En resumen, $scaler = StandardScaler()$ inicializa el objeto que luego se utilizará para estandarizar los datos.



### Explicación detallada

La línea $scaler = StandardScaler()$ crea una instancia del escalador estándar de **scikit-learn**, que se utiliza para normalizar/estandarizar los datos antes de entrenar modelos de machine learning.

### Funcionamiento

Transformación aplicada:

```python
# Para cada característica (columna) en tus datos:
valor_estandarizado = (valor_original - media) / desviación_estándar
```

### Resultado:

* Media = 0
* Desviación estándar = 1
* Distribución similar a una normal estándar

Ejemplo visual:



Antes de StandardScaler:

```python
# Datos originales (diferentes escalas)
edad = [25, 30, 35, 40, 45]          # Rango: 20-50
salario = [30000, 45000, 60000, 75000, 90000]  # Rango: 30,000-90,000
```

Problema: ¡El salario domina por tener valores más grandes!



**Después de Standardarizar**

```python
# Datos estandarizados
edad_estandarizada = [-1.41, -0.71, 0, 0.71, 1.41]
salario_estandarizado = [-1.41, -0.71, 0, 0.71, 1.41]

# Ahora ambas características tienen la misma escala
```

## parametro: tf.keras.layers.Dropout(0.3)

$$tf.keras.layers.Dropout(0.3)$$

El **Dropout**  es una técnica de regularización que ayuda a prevenir el sobreajuste (overfitting) en redes neuronales.

### Funcionamiento básico:

* Durante el entrenamiento: "Apaga" aleatoriamente un porcentaje de neuronas en cada iteración
* Durante la predicción: Usa todas las neuronas, pero escala los pesos

Con parámetro 0.3

```python
tf.keras.layers.Dropout(0.3)  # Apaga el 30% de las neuronas en cada paso de entrenamiento
```

### Analogía intuitiva:

Imagina que estás estudiando para un examen en grupo:

* Sin Dropout: Siempre confías en los mismos 2-3 estudiantes inteligentes
* Con Dropout: Cada día, algunos estudiantes no vienen, obligándote a confiar en otros

Resultado: El grupo se vuelve más robusto y menos dependiente de individuos específicos.

### optimizador, perdida y metricas

```python
model.compile(
        optimizer='adam',
        loss='sparse_categorical_crossentropy',  # Para etiquetas enteras
        metrics=['accuracy']
    )
```

Desglose:

1. $optimizer='adam'$: El optimizador es el algoritmo que ajusta los pesos de la red neuronal para minimizar la función de pérdida. 'adam' es un optimizador popular que combina las ventajas de otros dos optimizadores: RMSProp y Momentum. Es eficiente y requiere poca configuración, por lo que es una opción por defecto muy común.

2. **loss='sparse_categorical_crossentropy'**: La función de pérdida (loss function) mide qué tan buenas son las predicciones del modelo durante el entrenamiento. **'sparse_categorical_crossentropy'** es una función de pérdida para problemas de clasificación múltiple (multi-class) cuando las etiquetas están en forma de enteros (por ejemplo, 0, 1, 2) en lugar de one-hot encoding. **Ejemplo:** Si tenemos 3 clases y una muestra pertenece a la clase 2, la etiqueta es 2 (no [0, 0, 1]).Esta función calcula la entropía cruzada entre las etiquetas verdaderas y las predicciones.

3. $metrics=['accuracy']$: Las métricas se utilizan para monitorear el rendimiento del modelo durante el entrenamiento y la evaluación. 'accuracy' (precisión) es la fracción de predicciones correctas sobre el total de predicciones. Durante el entrenamiento, se mostrará la precisión después de cada época (o lote, dependiendo de la configuración).

¿Por qué 'sparse_categorical_crossentropy' y no 'categorical_crossentropy'?

- Si tus etiquetas están en one-hot encoding (vectores binarios), debes usar 'categorical_crossentropy'.
- Si tus etiquetas son enteros, usa 'sparse_categorical_crossentropy' para evitar tener que convertirlas a one-hot.

Ejemplo de etiquetas para **sparse_categorical_crossentropy**: [0, 2, 1, 2, 0] (para 3 clases)

Ejemplo de etiquetas para **categorical_crossentropy**: [ [1,0,0], [0,0,1], [0,1,0], [0,0,1], [1,0,0] ]

En el caso del dataset Iris, las etiquetas son 0, 1, 2 (setosa, versicolor, virginica), por lo que usamos sparse_categorical_crossentropy.

¿Qué hace el optimizador Adam?

- Adam (Adaptive Moment Estimation) ajusta la tasa de aprendizaje para cada peso de la red de manera individual.
- Combina el historial de gradientes (como Momentum) y la adaptación de la tasa de aprendizaje por la magnitud de los gradientes (como RMSProp).
- Parámetros típicos de Adam (que se pueden personalizar) son: learning_rate (tasa de aprendizaje), beta_1, beta_2, epsilon.

¿Qué es la precisión (accuracy)?

- accuracy = (número de predicciones correctas) / (total de predicciones)

Este código de compilación configura el modelo para que durante el entrenamiento use el optimizador Adam, la función de pérdida sparse_categorical_crossentropy y monitoree la precisión.

Es importante compilar el modelo antes de entrenarlo (con model.fit).

### model.compile() - Explicación completa

El método compile() en Keras/TensorFlow es donde configuras el proceso de aprendizaje de tu red neuronal. Es como "preparar el motor" antes de empezar a entrenar.

¿Qué hace model.compile()?

Configura tres componentes esenciales:

1. optimizer: Cómo el modelo aprende de los errores
2. loss: Cómo mide los errores
3. metrics: Qué métricas monitorear durante el entrenamiento