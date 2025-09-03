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

![En regresión lineal clásica (y en muchos modelos paramétricos similares).png](assets/En%20regresi%C3%B3n%20lineal%20cl%C3%A1sica%20%28y%20en%20muchos%20modelos%20param%C3%A9tricos%20similares%29.png)

![Where BO, B1 and B2 are the coefficients of the line that control the intercept and slope,.png](assets/Where%20BO%2C%20B1%20and%20B2%20are%20the%20coefficients%20of%20the%20line%20that%20control%20the%20intercept%20and%20slope%2C.png)

B0, B1, B2 = coeficientes de la línea  
X1, X2 = *input variables*

Los algoritmos paramétricos son utilizados en regresión lineal; para tener un modelo predictivo lo que tenemos que hacer es estimar los coeficientes de la función.

Ejemplos de *parametric machine learning algorithms* pueden ser:

- *Logistic Regression*
- *Linear Discriminant Analysis*
- *Perceptron*

**Parametric Machine Learning Algorithms Benefits vs. Limitations:**

![Benefits of Parametric Machine Learning Algorithms.png](assets/Benefits%20of%20Parametric%20Machine%20Learning%20Algorithms.png)

**NonParametric Machine Learning Algorithms:**

![Algorithms that do not make strong assumptions about the form of the mapping function are.png](assets/Algorithms%20that%20do%20not%20make%20strong%20assumptions%20about%20the%20form%20of%20the%20mapping%20function%20are.png)

**Examples of NonParametric Machine Learning Algorithms:**

![k-nearest neighbors algorithm.png](assets/k-nearest%20neighbors%20algorithm.png)

**NonParametric Machine Learning Algorithms Benefits vs. Limitations:**

![• Decision Trees like CART and C4.5.png](assets/%E2%80%A2%20Decision%20Trees%20like%20CART%20and%20C4.5.png)

![Benefits of Nonparametric Machine Learning Algorithms.png](assets/Benefits%20of%20Nonparametric%20Machine%20Learning%20Algorithms.png)

**Overfitting = sobreajuste**

**Supervised Machine Learning:**

![The majority of practical machine learning uses supervised learning. Supervised learning is.png](assets/The%20majority%20of%20practical%20machine%20learning%20uses%20supervised%20learning.%20Supervised%20learning%20is.png)

**Classification vs Regression:**

![• Classification A classification problem is when the output variable is a category, such.png](assets/%E2%80%A2%20Classification%20A%20classification%20problem%20is%20when%20the%20output%20variable%20is%20a%20category%2C%20such.png)

**Commons types of problem that are Supervised Machine Learning:**

![• Some common types of problems built on top of classification and regression include.png](assets/%E2%80%A2%20Some%20common%20types%20of%20problems%20built%20on%20top%20of%20classification%20and%20regression%20include.png)

**Unsupervised Machine Learning:**

![variables. The goal for unsupervised learning is to model the underlying structure or distribution.png](assets/variables.%20The%20goal%20for%20unsupervised%20learning%20is%20to%20model%20the%20underlying%20structure%20or%20distribution.png)

**Types of Unsupervised Machine Learning, Clustering vs Association:**

![• Clustering A clustering problem is where you want to discover the inherent groupings.png](assets/%E2%80%A2%20Clustering%20A%20clustering%20problem%20is%20where%20you%20want%20to%20discover%20the%20inherent%20groupings.png)

**Examples of Unsupervised Machine Learning Algorithms:**

![Some popular examples of unsupervised learning algorithms are.png](assets/Some%20popular%20examples%20of%20unsupervised%20learning%20algorithms%20are.png)

**SemiSupervised Machine Learning**

![Semi-Supervised Machine Learning.png](assets/Semi-Supervised%20Machine%20Learning.png)

*Unlabeled Data* = datos no etiquetados; básicamente, datos que a priori no tenemos información que los corresponda con ningún Y (o sea, con algún parámetro pasado al algoritmo, columna).

**Prediction Errors, 3 parts:**

![6.1 Overview of Bias and Variance.png](assets/6.1%20Overview%20of%20Bias%20and%20Variance.png)

**Irreducible Error:**

![Captura de pantalla 2025-08-19 a la(s) 4.16.50 p. m..png](assets/Captura%20de%20pantalla%202025-08-19%20a%20la%28s%29%204.16.50%E2%80%AFp.%C2%A0m..png)

**Bias Error:**

![Bias are the simplifying assumptions made by a model to make the target function casier to.png](assets/Bias%20are%20the%20simplifying%20assumptions%20made%20by%20a%20model%20to%20make%20the%20target%20function%20casier%20to.png)

**Low Bias:**

![• Low Bias Suggests more assumptions about the form of the target function..png](assets/%E2%80%A2%20Low%20Bias%20Suggests%20more%20assumptions%20about%20the%20form%20of%20the%20target%20function..png)

**Examples:**

![Decision Trees, k-Nearest Neigh-.png](assets/Decision%20Trees%2C%20k-Nearest%20Neigh-.png)

![bors and Support Vector Machines..png](assets/bors%20and%20Support%20Vector%20Machines..png)

**Variance Error:**

![data was used. The target function is estimated from the training data by a machine learning.png](assets/data%20was%20used.%20The%20target%20function%20is%20estimated%20from%20the%20training%20data%20by%20a%20machine%20learning.png)

![Machine learning algorithms that have a high variance are strongly influenoed by the specifics.png](assets/Machine%20learning%20algorithms%20that%20have%20a%20high%20variance%20are%20strongly%20influenoed%20by%20the%20specifics.png)

**Low Variance:**

![• Low Variance Suggests small changes to the estimate of the target function with changes.png](assets/%E2%80%A2%20Low%20Variance%20Suggests%20small%20changes%20to%20the%20estimate%20of%20the%20target%20function%20with%20changes.png)

**Examples:**

![Captura de pantalla 2025-08-19 a la(s) 4.34.54 p. m..png](assets/Captura%20de%20pantalla%202025-08-19%20a%20la%28s%29%204.34.54%E2%80%AFp.%C2%A0m..png)

![Regression, Linear Discriminant Analysis and Logistic Regression..png](assets/Regression%2C%20Linear%20Discriminant%20Analysis%20and%20Logistic%20Regression..png)

**High Variance:**

![• High Variance Suggests large changes to the estimate of the target function with.png](assets/%E2%80%A2%20High%20Variance%20Suggests%20large%20changes%20to%20the%20estimate%20of%20the%20target%20function%20with.png)

Algorithms that have a high flexibility (they make fewer assumptions on the target function, not approximating the target function to a known form) have HIGH bias.

**Examples:**

![Decision Trees, k-Nearest Neighbors and Support Vector.png](assets/Decision%20Trees%2C%20k-Nearest%20Neighbors%20and%20Support%20Vector.png)

![Machines..png](assets/Machines..png)

![• Parametric or linear machine learning algorithms often have a high bias but a low variance..png](assets/%E2%80%A2%20Parametric%20or%20linear%20machine%20learning%20algorithms%20often%20have%20a%20high%20bias%20but%20a%20low%20variance..png)

**Examples of how to treat the BIAS - VARIANCE TRADE OFF:**

![• The k-nearest neighbors algorithm has low bias and high variance, but the trade-off can.png](assets/%E2%80%A2%20The%20k-nearest%20neighbors%20algorithm%20has%20low%20bias%20and%20high%20variance%2C%20but%20the%20trade-off%20can.png)

![• Increasing the bias will decrease the variance..png](assets/%E2%80%A2%20Increasing%20the%20bias%20will%20decrease%20the%20variance..png)

**Overfitting (sobreajuste, sobrentrenamiento):**

![• That overfitting refers to learning the training data too well at the expense of not.png](assets/%E2%80%A2%20That%20overfitting%20refers%20to%20learning%20the%20training%20data%20too%20well%20at%20the%20expense%20of%20not.png)

![Overfitting is more likely with sonparametric and nonlinear models that have more Bexibility.png](assets/Overfitting%20is%20more%20likely%20with%20sonparametric%20and%20nonlinear%20models%20that%20have%20more%20Bexibility.png)

**Prunning a tree:**

Pruning un árbol (poda de un árbol de decisión) significa recortar ramas del árbol para que el modelo no sea tan complejo y no se quede memorizando detalles irrelevantes del *dataset* de entrenamiento.

**Tecniques to limit overfitting:**

![1. Use a resampling technique to estimate model accuracy..png](assets/1.%20Use%20a%20resampling%20technique%20to%20estimate%20model%20accuracy..png)

![2. Hold back a validation dataset..png](assets/2.%20Hold%20back%20a%20validation%20dataset..png)

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

![That underfitting refers to failing to learn the problem from the training data sufficiently..png](assets/That%20underfitting%20refers%20to%20failing%20to%20learn%20the%20problem%20from%20the%20training%20data%20sufficiently..png)

![7.4 Underfitting in Machine Learning.png](assets/7.4%20Underfitting%20in%20Machine%20Learning.png)

**Inductive Learning:**

![the learning of the target function from training data.png](assets/the%20learning%20of%20the%20target%20function%20from%20training%20data.png)

**Generalization:**

![Generalization refers to how well the concepts learned by a machine learning model apply.png](assets/Generalization%20refers%20to%20how%20well%20the%20concepts%20learned%20by%20a%20machine%20learning%20model%20apply.png)

![to specific examples not seen by the model when it was learning..png](assets/to%20specific%20examples%20not%20seen%20by%20the%20model%20when%20it%20was%20learning..png)

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
