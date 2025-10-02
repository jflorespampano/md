---
categoría: ia
tipo: conceptos
---
## Umbral (Thresholds) y  matriz de confusión

Supongamos que tiene un modelo de regresión logística para la detección de correo no deseado que predice un valor entre 0 y 1, que representa la probabilidad de que un correo electrónico determinado sea spam. Una predicción de 0,50 significa un 50 % de probabilidad de que el correo sea spam, una predicción de 0,75 significa un 75 % de probabilidad de que sea spam, y así sucesivamente.

Quiere implementar este modelo en una aplicación de correo electrónico para filtrar el spam en una carpeta de correo independiente. Para ello, necesita convertir el resultado numérico bruto del modelo (p. ej., 0,75) a una de dos categorías: "spam" o "no spam".

Para realizar esta conversión, se elige una probabilidad umbral, denominada umbral de clasificación. Los ejemplos con una probabilidad superior al valor umbral se asignan a la clase positiva, la clase que se está probando (en este caso, spam). Los ejemplos con una probabilidad menor se asignan a la clase negativa, la clase alternativa (en este caso, no spam).

## Matriz de confusión

La puntuación de probabilidad no es la realidad ni la verdad fundamental. Hay cuatro resultados posibles para cada salida de un clasificador binario. En el ejemplo del clasificador de spam, si se presenta la verdad fundamental en columnas y la predicción del modelo en filas, el resultado es la siguiente tabla, denominada matriz de confusión:

|                     | Positivo real      | Negativo real       |
| ------------------- | ------------------ | ------------------- |
| Predicción positiva | True Positive (TP) | False Positivo (FP) |
| Predicción negativa | False Negative(FN) | True Negative (TN)  |

Observe que el total de cada fila muestra todos los positivos predichos (TP + FP) y todos los negativos predichos (FN + TN), independientemente de su validez. Por otro lado, el total de cada columna muestra todos los positivos reales (TP + FN) y todos los negativos reales (FP + TN), independientemente de la clasificación del modelo.

Cuando el total de positivos reales no se acerca al total de negativos reales, el conjunto de datos está desequilibrado. Un ejemplo de un conjunto de datos desequilibrado podría ser un conjunto de miles de fotos de nubes, donde el tipo de nube poco común que le interesa, por ejemplo, las nubes volutus, solo aparece unas pocas veces.

Los diferentes umbrales suelen dar lugar a diferentes números de verdaderos y falsos positivos, así como de verdaderos y falsos negativos.

En clasificación binaria, un modelo normalmente devuelve una **probabilidad** entre 0 y 1. El umbral determina a partir de qué valor consideramos una predicción como "positiva":

```python
# Ejemplo conceptual
probabilidad = modelo.predict_proba(x)[0][1]  # Ej: 0.75

if probabilidad >= umbral:
    predicción = "Positivo"
else:
    predicción = "Negativo"
```

Ejemplo con diferentes umbrales:

|Instancia|Probabilidad Real|**Umbral 0.5**|**Umbral 0.7**|**Umbral 0.3**|
|---|---|---|---|---|
|1|0.85|✅ VP|✅ VP|✅ VP|
|2|0.65|✅ VP|❌ FN|✅ VP|
|3|0.45|❌ VN|❌ VN|✅ FP|
|4|0.75|✅ VP|✅ VP|✅ VP|
|5|0.25|❌ VN|❌ VN|❌ VN|
|6|0.55|✅ VP|❌ FN|✅ VP|
|7|0.35|❌ VN|❌ VN|✅ FP|
|8|0.90|✅ VP|✅ VP|✅ VP|
|9|0.15|❌ VN|❌ VN|❌ VN|
|10|0.60|✅ VP|❌ FN|✅ VP|
**Resultados por umbral:**

- **Umbral 0.5**: 5 VP, 3 VN, 0 FP, 2 FN
- **Umbral 0.7**: 3 VP, 3 VN, 0 FP, 4 FN
- **Umbral 0.3**: 6 VP, 2 VN, 2 FP, 0 FN