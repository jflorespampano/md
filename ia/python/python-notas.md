---
categoría: programación
tipo: pythom
---
# notas
## entornos virtuales

```sh
#Instalar paquete
pip install virtualenv
#desinstalar
pip uninstall virtualenv
# mostrar todos los modulos instalados
pip freeze

# crear entorno virtual en una carpeta
cd carpeta
# Crear entorno virtual
python -m venv myenv
# Activar entorno (Windows)
myenv\Scripts\activate

# Activar entorno (Linux/Mac)
# este no: source myenv/bin/activate
source prueba/scripts/activate

# ver mi entorno virtual
echo $VIRTUAL_ENV

#desactiva entorno virtual
deactivate
```

Bibliotecas necesarias

```sh

# instalar sklearn en el entorno activo
pip install scikit-learn

# instalar 
pip install matplotlib
```

## Ejemplos

```python
import numpy as np
import matplotlib.pyplot as plt

```
devuelve un arreglo de números enteros que son mayores o iguales a (>=) el primer número y menores que (<) el segundo número.

```python
np.arange(n1,n2)
```

puedes usar una tercera variable que proporciona un tamaño de paso para que la función regrese. Pasar 2 como tercera variable devolverá cada segundo número en el rango, pasar 5 como tercera variable devolverá cada quinto número en el rango:

```python
np.arange(n1,n2,n3)
```

```python
np.zeros(4)
np.ones(5)

# linespace: 0 l inicio, 1 el fin, 10 numero de subintervalos
np.linspace(0, 1, 10)
np.eye(50) ## devuelve un arreglo identidad de 50*50

#Devuelve una muestra de números aleatorios entre 0 y 1.
np.random.rand(sample_size) 
#Devuelve una muestra de números enteros que son mayores o iguales que 'low' y menores que 'high' 
np.random.randint(low, high, sample_size)
arr = np.array([0,1,2,3,4,5])
arr.reshape(2,3)
arr.shape # ahora Devuelve (2,3)

simple_array = [1, 2, 3, 4]
simple_array.max() #Devuelve 4
simple_array.argmax() #Devuelve  indice de maximo valor3
simple_array.min() #Devuelve 1
simple_array.argmin() #Devuelve 0
```


## operaciones en numpy

```python

2+arr
arr + arr
arr - 10
arr / 2

np.sqrt(arr)
np.exp(arr) # e elevado a la cada elemento de arr

arr = np.random.rand(5)
arr = np.round(arr, 2) #  redondear a 2 decimales

arr[:] #Retorna el arreglo completo: array([0.69, 0.94, 0.66, 0.73, 0.83])

arr[1:] #Devuelve array([0.94, 0.66, 0.73, 0.83])

arr[1:4] #Devuelve array([0.94, 0.66, 0.73])
```


## PIP

```sh
pip install pandas
# Verifica tu versión actual de pandas, ejemplo: 1.5.2
pip show pandas

# Actualiza pandas en tu ordenador
pip install --upgrade pandas

# Verifica tu versión de pandas actualizada, ejemplo: 2.0.2
pip show pandas
python -m venv sklearn-env
```

## refs

1. [numpy](https://www.freecodecamp.org/espanol/news/la-guia-definitiva-del-paquete-numpy-para-computacion-cientifica-en-python/)
2. [colabs](https://colab.research.google.com/)
3. [pandas](https://4geeks.com/es/how-to/instalar-pandas-python)