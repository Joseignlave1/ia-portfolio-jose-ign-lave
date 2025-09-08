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

![En regresión lineal clásica](../assets/en-regresion-lineal-clasica.png)

![Where BO, B1 and B2](../assets/coefficients-b0-b1-b2.png)

B0, B1, B2 = coeficientes de la línea  
X1, X2 = *input variables*

Los algoritmos paramétricos son utilizados en regresión lineal; para tener un modelo predictivo lo que tenemos que hacer es estimar los coeficientes de la función.

Ejemplos de *parametric machine learning algorithms* pueden ser:

- *Logistic Regression*
- *Linear Discriminant Analysis*
- *Perceptron*

**Parametric Machine Learning Algorithms Benefits vs. Limitations:**

![Benefits of Parametric](../assets/benefits-parametric.png)

**NonParametric Machine Learning Algorithms:**

![Algorithms that do not make strong assumptions](../assets/nonparametric-no-strong-assumptions.png)

**Examples of NonParametric Machine Learning Algorithms:**

![k-nearest neighbors](../assets/knn-algorithm.png)

**NonParametric Machine Learning Algorithms Benefits vs. Limitations:**

![Decision Trees CART](../assets/decision-trees-cart.png)

![Benefits of Nonparametric](../assets/benefits-nonparametric.png)

**Overfitting = sobreajuste**

**Supervised Machine Learning:**

![Supervised Learning](../assets/supervised-learning.png)

**Classification vs Regression:**

![Classification](../assets/classification.png)

**Commons types of problem that are Supervised Machine Learning:**

![Some common types](../assets/classification-regression-types.png)

**Unsupervised Machine Learning:**

![Variables](../assets/unsupervised-variables.png)

**Types of Unsupervised Machine Learning, Clustering vs Association:**

![Clustering](../assets/clustering.png)

**Examples of Unsupervised Machine Learning Algorithms:**

![Examples unsupervised](../assets/unsupervised-examples.png)

**SemiSupervised Machine Learning**

![Semi-Supervised](../assets/semi-supervised.png)

*Unlabeled Data* = datos no etiquetados; básicamente, datos que a priori no tenemos información que los corresponda con ningún Y (o sea, con algún parámetro pasado al algoritmo, columna).

**Prediction Errors, 3 parts:**

![6.1 Overview of Bias and Variance](../assets/overview-bias-variance.png)

**Irreducible Error:**

![Captura 1](../assets/irreducible-error.png)

**Bias Error:**

![Bias assumptions](../assets/bias-simplifying.png)

**Low Bias:**

![Low Bias](../assets/low-bias.png)

**Examples:**

![Decision Trees](../assets/decision-trees-knn.png)

![Support Vector](../assets/svm-others.png)

**Variance Error:**

![Data variance](../assets/variance-estimate.png)

![High variance algo](../assets/high-variance.png)

**Low Variance:**

![Low variance](../assets/low-variance.png)

**Examples:**


![Regression LDA](../assets/regression-lda-logistic.png)

**High Variance:**

![High variance](../assets/high-variance-suggests.png)

Algorithms that have a high flexibility (they make fewer assumptions on the target function, not approximating the target function to a known form) have HIGH bias.

**Examples:**

![Machines](../assets/machines.png)

![Parametric bias](../assets/parametric-high-bias.png)

**Examples of how to treat the BIAS - VARIANCE TRADE OFF:**

![k-nearest tradeoff](../assets/knn-tradeoff.png)

![Increasing bias](../assets/increasing-bias.png)

**Overfitting (sobreajuste, sobrentrenamiento):**

![Overfitting](../assets/overfitting-definition.png)

![Overfitting flexibility](../assets/overfitting-flexibility.png)

**Prunning a tree:**

Pruning un árbol (poda de un árbol de decisión) significa recortar ramas del árbol para que el modelo no sea tan complejo y no se quede memorizando detalles irrelevantes del *dataset* de entrenamiento.

**Tecniques to limit overfitting:**

![Resampling](../assets/resampling-technique.png)

![Validation dataset](../assets/hold-back-validation.png)

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

![Underfitting](../assets/underfitting.png)

![Underfitting 7.4](../assets/underfitting-ml.png)

**Inductive Learning:**

![Inductive](../assets/learning-target-function.png)

**Generalization:**

![Generalization](../assets/generalization.png)

![Generalization examples](../assets/generalization-examples.png)

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
