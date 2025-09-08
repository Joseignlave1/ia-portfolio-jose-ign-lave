---
title: "Entrada 04 — Resumen del primer IRAT"
date: 2025-01-01
---

# Entrada 04 — Resumen del primer IRAT

## Contexto
Realicé un resumen para el primer IRAT del curso; esto me permitió afianzar mis conocimientos
de una mejor manera, aprendiendo sobre la introducción a *machine learning* y en qué se basan los modelos de *machine learning*.

## Objetivos
- Poder comprender el concepto de *Predictive Modeling*.
- Comprender qué significa el concepto de algoritmos paramétricos y cuándo es conveniente utilizarlos.
- Comprender qué significa el concepto de algoritmos no paramétricos y cuándo es conveniente utilizarlos.
- Comprender el concepto de *overfitting* y *underfitting*.
- Comprender las técnicas para prevenir el *overfitting*.
- Comprender el concepto de *machine learning* supervisado, semi-supervisado vs. no supervisado.
- Comprender el concepto de *Clustering* y *Association* en *machine learning* no supervisado.
- Entender la diferencia entre *low bias* y *high bias*.
- Entender el *variance error*.

## Actividades (con tiempos estimados)
- Leer y analizar las lecturas — 1 hora y media.
- Realizar un resumen de las lecturas.

## Desarrollo

Procedo a adjuntar el resumen del IRAT:

**IRAT I IA:**

*Predictive modeling:* subfield of machine learning focused on making predictions.

f = *target function*  
y = *output value*, el *output* que va a devolver el modelo.  
y = f(x) + e  
x = *input data*, parámetros que le pasamos al modelo.  
e = *irreducible error*, no importa qué tan cerca lleguemos de estimar la *target function*, nunca vamos a poder reducir este error. e es independiente de X.

*Predictive modelling*, Y = f(x): hacemos predicciones de Y para un nuevo x; nuestro objetivo es realizar la predicción más acertada de y dado un x.

No estamos interesados en la forma de la función f; solo queremos que haga predicciones acertadas.

Podríamos aprender el mapeo de y = f(x) para aprender más acerca de las relaciones de los datos; esto se llama **estadística inferencial**.

**Parametric Algorithm** = simplifican f a una forma conocida; el número de parámetros a estimar es fijo, independiente de la cantidad de datos.

**Parametric Model** = modelo de aprendizaje que resume datos, con una cantidad de parámetros de longitud fija (independientemente del número de ejemplos entrenados). Siempre la cantidad de parámetros a estimar va a ser p + 1, siendo p la cantidad de columnas de los datos que le pasamos al algoritmo y 1 = b0, o sea *bias* (error de intercepto).

![En regresión lineal clásica](../assets/En regresión lineal clásica (y en muchos modelos paramétricos similares).png)

![Where BO, B1 and B2](../assets/Where BO, B1 and B2 are the coefficients of the line that control the intercept and slope,.png)

B0, B1, B2 = coeficientes de la línea  
X1, X2 = *input variables*

Los algoritmos paramétricos son utilizados en regresión lineal; para tener un modelo predictivo lo que tenemos que hacer es estimar los coeficientes de la función.

Ejemplos de *parametric machine learning algorithms* pueden ser:

- *Logistic Regression*
- *Linear Discriminant Analysis*
- *Perceptron*

**Parametric Machine Learning Algorithms Benefits vs. Limitations:**

![Benefits of Parametric](../assets/Benefits of Parametric Machine Learning Algorithms.png)

**NonParametric Machine Learning Algorithms:**

![Algorithms that do not make strong assumptions](../assets/Algorithms that do not make strong assumptions about the form of the mapping function are.png)

**Examples of NonParametric Machine Learning Algorithms:**

![k-nearest neighbors](../assets/k-nearest neighbors algorithm.png)

**NonParametric Machine Learning Algorithms Benefits vs. Limitations:**

![Decision Trees CART](../assets/Decision Trees, k-Nearest Neigh-.png)

![Benefits of Nonparametric](../assets/Benefits of Nonparametric Machine Learning Algorithms.png)

**Overfitting = sobreajuste**

**Supervised Machine Learning:**

![Supervised Learning](../assets/The majority of practical machine learning uses supervised learning. Supervised learning is.png)

**Classification vs Regression:**

![Classification](../assets/• Classification A classification problem is when the output variable is a category, such.png)

**Commons types of problem that are Supervised Machine Learning:**

![Some common types](../assets/• Some common types of problems built on top of classification and regression include.png)

**Unsupervised Machine Learning:**

![Variables](../assets/variables. The goal for unsupervised learning is to model the underlying structure or distribution.png)

**Types of Unsupervised Machine Learning, Clustering vs Association:**

![Clustering](../assets/• Clustering A clustering problem is where you want to discover the inherent groupings.png)

**Examples of Unsupervised Machine Learning Algorithms:**

![Examples unsupervised](../assets/Some popular examples of unsupervised learning algorithms are.png)

**SemiSupervised Machine Learning**

![Semi-Supervised](../assets/Semi-Supervised Machine Learning.png)

*Unlabeled Data* = datos no etiquetados; básicamente, datos que a priori no tenemos información que los corresponda con ningún Y (o sea, con algún parámetro pasado al algoritmo, columna).

**Prediction Errors, 3 parts:**

![Bias and Variance](../assets/6.1 Overview of Bias and Variance.png)

**Irreducible Error:**

![Captura 1](../assets/Captura de pantalla 2025-08-19 a la(s) 4.16.50 p. m..png)

**Bias Error:**

![Bias assumptions](../assets/Bias are the simplifying assumptions made by a model to make the target function casier to.png)

**Low Bias:**

![Low Bias](../assets/• Low Bias Suggests more assumptions about the form of the target function..png)

**Examples:**

![Decision Trees](../assets/Decision Trees, k-Nearest Neigh-.png)

![Support Vector](../assets/bors and Support Vector Machines..png)

**Variance Error:**

![Data variance](../assets/data was used. The target function is estimated from the training data by a machine learning.png)

![High variance algo](../assets/Machine learning algorithms that have a high variance are strongly influenoed by the specifics.png)

**Low Variance:**

![Low variance](../assets/• Low Variance Suggests small changes to the estimate of the target function with changes.png)

**Examples:**

![Captura 2](../assets/Captura de pantalla 2025-08-19 a la(s) 4.34.54 p. m..png)

![Regression LDA](../assets/Regression, Linear Discriminant Analysis and Logistic Regression..png)

**High Variance:**

![High variance](../assets/• High Variance Suggests large changes to the estimate of the target function with.png)

Algorithms that have a high flexibility (they make fewer assumptions on the target function, not approximating the target function to a known form) have HIGH bias.

**Examples:**

![Decision Trees 2](../assets/Decision Trees, k-Nearest Neighbors and Support Vector.png)

![Machines](../assets/Machines..png)

![Parametric bias](../assets/• Parametric or linear machine learning algorithms often have a high bias but a low variance..png)

**Examples of how to treat the BIAS - VARIANCE TRADE OFF:**

![k-nearest tradeoff](../assets/• The k-nearest neighbors algorithm has low bias and high variance, but the trade-off can.png)

![Increasing bias](../assets/• Increasing the bias will decrease the variance..png)

**Overfitting (sobreajuste, sobrentrenamiento):**

![Overfitting](../assets/• That overfitting refers to learning the training data too well at the expense of not.png)

![Overfitting flexibility](../assets/Overfitting is more likely with sonparametric and nonlinear models that have more Bexibility.png)

**Prunning a tree:**

Pruning un árbol (poda de un árbol de decisión) significa recortar ramas del árbol para que el modelo no sea tan complejo y no se quede memorizando detalles irrelevantes del *dataset* de entrenamiento.

**Tecniques to limit overfitting:**

![Resampling](../assets/1. Use a resampling technique to estimate model accuracy..png)

![Validation dataset](../assets/2. Hold back a validation dataset..png)

**Resampling vs Holding a Validation dataset:**

Resampling (*k*-fold cross validation)  
* Idea: dividir tu *dataset* en *k* partes.  
* Cada vez entrenás el modelo con *k-1* partes y lo probás con la parte que quedó afuera.  
* Repetís este proceso *k* veces, cambiando cuál parte queda afuera.  
* Así obtenés *k* estimaciones de rendimiento, y el promedio es un estimador más robusto de cómo funcionará el modelo con datos nuevos.  
* Ventaja: usás todos los datos tanto para entrenar como para validar, en diferentes momentos.

2. *Validation dataset*  
* Idea: separar desde el principio una parte del *dataset* (no se usa en el entrenamiento).  
* Entrenás y tunéas el modelo con el resto.  
* Al final, lo probás en este *dataset* reservado, para tener una evaluación “honesta” del desempeño real.  
* Ventaja: simula mejor el escenario de datos realmente nuevos.

**Diferencia clave**  
* *Cross validation*: sirve para elegir y ajustar el modelo (estimación interna).  
* *Validation dataset*: sirve para la evaluación final (medir lo que podría pasar en producción).

**Underfitting:**

![Underfitting](../assets/That underfitting refers to failing to learn the problem from the training data sufficiently..png)

![Underfitting 7.4](../assets/7.4 Underfitting in Machine Learning.png)

**Inductive Learning:**

![Inductive](../assets/the learning of the target function from training data.png)

**Generalization:**

![Generalization](../assets/Generalization refers to how well the concepts learned by a machine learning model apply.png)

![Generalization examples](../assets/to specific examples not seen by the model when it was learning..png)

All the machine learning models want to have the best possible generalization.

## Evidencias
- Enlace a material o capturas en `docs/assets/`.

## Reflexión
Considero que lo más desafiante fue entender cuándo es conveniente utilizar los algoritmos paramétricos, ya que
son más rápidos al simplificar f a una forma conocida, pero rara vez aciertan la predicción de la función f,
por lo que resultan menos eficientes. También el hecho de cómo manejar *unlabeled data*, ya que no tenemos información
que los relacione a ninguno de los atributos del *dataset*. También me pareció muy interesante el concepto de *overfitting*, ya
que es algo que nos puede pasar y que entiendo que en la industria puede costar mucho dinero revertir; por ello
considero que es valioso entender el concepto y las técnicas para prevenirlo.

## Próximos pasos
Procedí a realizar la tarea 4 y posteriormente realicé los cursos en Kaggle de *Data Visualization*, *Intro to Machine Learning* e
*Intermediate Machine Learning*.
