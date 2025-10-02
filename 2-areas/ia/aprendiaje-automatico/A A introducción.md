---
categoría: ia
tipo: conceptos
---

# Aprendizaje automático

Los sistemas de AA aprenden cómo combinar entradas para producir predicciones útiles sobre datos nunca antes vistos. Entrenar un modelo significa aprender (determinar) valores correctos para todas los ejemplos(x) y las ordenadas al origen (y) de los ejemplos etiquetados.

En un aprendizaje supervisado, el algoritmo de un aprendizaje automático construye un modelo al examinar varios ejemplos e intentar encontrar un modelo que minimice la pérdida. Este proceso se denomina minimización del riesgo empírico.

## Notación

Revisemos alguna notación usada en este documento

* ***Atributo** (o característica) es una variable de entrada $x1,x2,x3,...,xn$
* ***Ejemplo** es una instancia de datos en particular $x$ se coloca en negrita para indicar que es un vector.

  
los ejemplos se dividen en:

- **etiquetados** y
- **no etiquetados**

  

Los ejemplos etiquetados son ejemplos de los cuales sabes la respuesta, es decir dado un ***x*** conoce el valor ***y*** asociado, los ejemplos no etiquetados son aquellos de los cuales desconoces la respuesta, es decir dado un ***x*** desconocemos su valor ***y*** asociado.

  
### Notación para Ejemplos etiquetados

* Ejemplo etiquetado: {características, etiqueta} o (x,y)
* labeled examples: {features, label} or (x,y)

Los ejemplos etiquetados se usan para entrenar el modelo.

### Notación para Ejemplos no etiquetados

* unlabeled examples: {características, ?} o (x,?)

### **Modelo**. 

Define la relación entre los atributos y la etiqueta. Por ejemplo, un modelo de detección de spam podría asociar de manera muy definida determinados atributos con \"es spam\". Que el correo tenga un origen específico o que contiene la palabra: 'ganaste', o contenga la palabra: ´gran promoción´ podría indicar que es spam.

Destaquemos dos fases en el ciclo de un modelo:

***Entrenamiento*** significa crear o enseñar al modelo. Es decir, le muestras ejemplos etiquetados al modelo y permites que este aprenda gradualmente las relaciones entre los atributos y la etiqueta.

***Inferencia*** significa aplicar el modelo entrenado a ejemplos sin etiqueta. Es decir, usas el modelo entrenado para realizar predicciones útiles (y\'). Por ejemplo, durante la inferencia, puedes predecir valores para nuevos ejemplos sin etiqueta.

Observe que un modelo se usa para predecir (inferir) valores (etiquetas y) desconocidos para ejemplos (x) dados. Estas predicciones pueden ser para valores continuos o discretos.

[[Regresión lineal]]