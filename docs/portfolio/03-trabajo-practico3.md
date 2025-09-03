---
title: "Entrada 03 — Segundo Trabajo Práctico"
date: 2025-01-01
---

# Entrada 03 — Segundo Trabajo Práctico~~
~~
## Contexto
Segundo trabajo práctico del curso. En esta ocasión empezamos a entender el concepto de Feature Engineering, y a entender conceptualmente cómo funcionan tipos de modelos, empezando por los de regresión logística "Logistic Regression",
a la vez que aprendimos qué es un Dummy Classifier, el método train_test_split, y métricas de evaluación.

## Objetivos
- Entender en qué se basa y cómo funciona un modelo de regresión logística
- Entender en qué casos me conviene y en cuáles no utilizar un modelo de regresión logística
- Entender qué significa y para qué sirve un dummy classiffier
- Entender qué significa y para qué se utiliza el método de train_test_split
- Entender el concepto de métricas de evaluación, en qué se basa cada métrica de las planteadas
- Entender cuándo me conviene utilizar cada métrica, teniendo en cuenta el contexto del problema a resolver.

## Actividades (con tiempos estimados)
- Investigación de Scikit-learn (10 min)
- Preprocesamiento y features (15 min)
- Modelo base y baseline (20 min)
- Responder preguntas finales planteadas por el docente (20 min)

## Desarrollo
Primero procedí a realizar una investigación de qué era un modelo de Regresión Logística y en qué casos me conviene utilizarlo,
luego empecé a investigar acerca de sus parámetros y qué significan cada uno tomando como base la documentación oficial de scikit-learn.

Después investigué el concepto de dummy classifier, entendí para qué se utiliza, y pude aprender sobre las diferentes estrategias mediante el
cual podemos configurarlo para luego compararlo con nuestro modelo.

Más adelante investigué sobre el método train_test_split, para qué sirve, cuándo debo utilizarlo y cuáles son los porcentajes óptimos del porcentaje
de los datos los cuales deben ser divididos en el dataset entre train y test, en otras palabras, cuál es el porcentaje de los datos de nuestro dataset
que conviene utilizar para test.

También indagué acerca del concepto de métricas de evaluación, para luego adentrarme en el concepto de las métricas de evaluación de la función
classification_report, para luego profundizar en el concepto de cada una (precision, recall, f1-score, Support, Accuracy).

Luego entendí el concepto de matriz de confusión, teniendo en cuenta la cantidad de verdaderos positivos, falsos positivos, verdaderos negativos, falsos negativos, haciendo una analogía de
estos conceptos a lo aprendido en Probabilidad y Estadística en la parte de test de hipótesis con el error de tipo I y el error de tipo II.

Después procedí a responder el resto de las preguntas.

Por último, realicé observaciones generales pudiendo interpretar las métricas, y más importante, teniendo contexto de cuándo utilizar cada una de ellas.

Procedo a adjuntar las preguntas del trabajo práctico.
""""
LogisticRegression:

¿Qué tipo de problema resuelve?

El Logistic regression es un modelo lineal el cuál resuelve
problemas de tipo clasificación.

Es "lineal" debido a que asume que la salida (el logit de la probabilidad)
va a ser una combinación lineal de las variables de entrada.

¿Qué parámetros importantes tiene?

Considero que los parámetros más importantes son: penalty, dualbool, tol, class_weight (útil si las muestras (registros) de las clases están desbalanceadas), solver (algoritmo que se va a utilizar en el problema de optimización), max_iter

//penalty = {‘l1’, ‘l2’, ‘elasticnet’, None}, default=’l2’
Especifica qué tipo de penalty será agregado.

None: no se agrega penalty

'l2': añade un penalty de tipo L2, es la opción por default

'l1': añade un penalty de tipo L1.

'elasticnet': Añade un penalty de tipo L1 y un penalty de tipo L2.



'elasticnet': both L1 and L2 penalty terms are added.
Entiendo penalty como "regularización", un término extra que se agrega
a la función de costo, para evitar que los datos crezcan demasiado
y el modelo se sobreajuste con los datos de entrenamiento.

Sobreajuste = entiendo que esto se refiere a cuando el modelo aprende demasiado bien los datos de entrenamiento,
lo que hace que genere patrones exactos para mi dataset, pero falle al generalizar.

Ejemplo: si queremos predecir si alguien va a comprar o no una hamburguesa, un modelo con un alto grado de sobreajuste
podría aprender algo como:
“Si la persona tiene 27.5 años y pesa 72.3 kg, siempre compra hamburguesa”.
Lo que funcionaría bien para un dataset específico, pero no al generalizar.

//dualbool, default=False

Define cómo se resuelve el problema de optimización en la regresión logística

tiene dos formas:

Primal (regularized, dual=False)

Optimiza directamente sobre los coeficientes W

Escala mucho mejor cuando hay más ejemplos que features (o sea cuando hay más cantidad de filas que columnas en el dataset)

Dual (constrained, dual=True)

Reformula el problema en términos de multiplicadores de Lagrange en lugar de los pesos w

Más eficiente cuando tenemos más features que ejemplos (más columnas que filas en nuestro dataset)
Solo está implementado para penalty='l2' con solver='liblinear'.

tol: float, default=1e-4 (10 elevado a la -4)

Tolerancia para el criterio de parada del algoritmo,
en cada iteración calcula cuánto mejora la función objetivo.

si la mejora es menor que tol el algoritmo se detiene, ya que se considera que el modelo ya convergió, encontró un conjunto de parámetros (w y w0) tal que la función
de costo no mejora significativamente al realizar nuevas iteraciones.

class_weight = pesos asociados con las clases, si no es especificado, todas las clases van a tener peso 1.

Entiendo peso como cuánta importancia tiene esa clase a la hora de que el algoritmo vaya a predecir la solución al problema.

solver = Algoritmo que se va a utilizar para resolver el problema.

parámetros importantes penalty, dualbool, tol, class_weight, solver (algoritmo que se va a utilizar en el problema de optimización), max_iter

//max_iter
Máximo número de iteraciones que puede realizar el solver para que el algoritmo converga

¿Cuándo usar solver='liblinear' vs otros solvers?
El parámetro solver se refiere al algoritmo que se va a utilizar para resolver el problema

Se recomienda utilizar 'liblinear' para datasets que son pequeños, y
'sag' o 'saga' para datasets con una gran cantidad de datos, ya que son algoritmos más rápidos.

Esto es debido a que 'liblinear' utiliza algoritmos de optimización cuadrática O(n al cuadrado) en tiempo de ejecución,
por lo que a medida que el dataset crece se vuelve lento.

En cambio sag y saga utilizan algoritmos de tipo "gradiente estocástico" los cuáles tienen una complejidad de O(n features) por iteración, siendo features = número de columnas

DummyClassifier:

¿Para qué sirve exactamente?

Realiza predicciones que ignoran las features (columnas) pasadas al algoritmo como input.
Entiendo que sirve para realizar clasificaciones randoms y poder compararlas con las clasificaciones realizadas por otros classifiers más complejos.

Si comparamos nuestro modelo classifier vs un DummyClassifier y este no lo mejora, entonces es una buena señal de que nuestro modelo está clasificando incorrectamente.

¿Qué estrategias de baseline ofrece?
Todas las estrategias hacen predicciones que ignoran los valores de x, o sea las features pasadas como input al algoritmo.

Las estrategias "stratified" y "uniform" nos dan predicciones no determinísticas (no podemos determinar qué va a predecir el algoritmo),
pueden volverse determinísticas si seteamos el parámetro random_state.

las otras estrategias son naturalmente determinísticas, y una vez que realicen la determinación, siempre van a devolver la misma constante
por cualquier valor de x (cualquier feature que le pasemos como input al algoritmo)

Estrategias:
“most_frequent”: La predicción siempre retorna la clase más frecuente (la que tenga más peso), el método predict_proba devuelve un
vector one-hot, el cuál tiene una probabilidad de 1 para la clase más frecuente y 0 para las demás.

"Prior": Siempre se predice la clase más frecuente (similar a most_frequent) pero en este caso
predict_proba devuelve la distribución empírica de las clases en el conjunto de entrenamiento.
por ejemplo si tenemos A: 70%, B: 20%, C:10%
entonces predict_proba = [0.7, 0.2, 0.1]

Stratified: Genera vectores one-hot aleatorios, siguiendo la
distribución de clases observada (muestrea una multinomial con esas probabilidades)

predict_proba = Devuelve un arreglo, similar a prior, pero poniendo peso 1 de forma aleatoria a cualquiera de las clases.

ejemplo:
70%, B: 20%, C:10%
predict_proba = [1,0,0] // 1 iteración, esto es totalmente aleatorio.
                [0,1,0]
                [0,0,1]

uniform: Genera predicciones randoms con probabilidad uniforme entre las clases de entrenamiento del modelo.

constant: Siempre predice una constante la cuál es provista por el usuario.

útil si se elige la clase no prioritaria como constante, para que métricas como recall (sensibilidad) o F1 de esa clase no sean 0
ya que si utilizamos por ejemplo la estrategia most_frequent, nunca la vamos a predecir.

¿Por qué es importante tener un baseline? Entiendo que es importante tenerlo para tener un punto de comparación con nuestro modelo,
ya que si por ejemplo comparamos el rendimiento de nuestro modelo con un dummyClassifier y vemos que el porcentaje
de predicciones acertadas es similar, entonces algo anda mal.

train_test_split:
Es una función de scikit-learn que automatiza el proceso de
dividir un dataset en dos conjuntos: train set (conjunto de datos de entrenamiento)
y test set (los datos utilizados para probar al modelo)

¿Qué hace el parámetro stratify?
El parámetro stratify modela la proporción de registros que van a estar en test y train, en relación al peso de las clases

si stratify = none, esta división se hace totalmente aleatoria, lo que puede ocasionar que en test o en train haya pocos registros de una clase

Mientras que si stratify = y, la división se realiza teniendo en cuenta la proporción relativa que tenían las clases en el dataset completo.

¿Por qué usar random_state?
Es recomendable utilizar random_state ya que nos permite tener una "semilla", orden aleatorio para la distribución de los datos tanto en train como test
si no lo utilizamos puede pasar que por ejemplo si nuestro dataset está ordenado (tiene primero todos los elementos de la clase a y segundo todos los elementos de la clase b)
entonces train tendría solo elementos de la clase A y test tendría solo elementos de la clase B.

¿Qué porcentaje de test es recomendable?
Entiendo que el porcentaje recomendado es el 25% de los datos del dataset.

Métricas de evaluación:
¿Qué significa cada métrica en classification_report?

precision = De todos los casos que el modelo marcó como positivo, cuántos realmente lo eran?

recall = De todos los casos positivos, cuántos encontró el modelo (pudo predecir correctamente que eran positivos), esto se refiere a
positivos / (positivos + falsos negativos)

f1-score = Se utiliza para saber cuán balanceado está el modelo, o sea, qué tan bien logra el balance entre el recall y la precisión, siempre da como resultado un número entre 0 y 1,
entiendo que al final esta métrica se utiliza para medir qué tan bien performa el modelo.

Support = Representa la cantidad de "registros" (concurrencias) de cada clase

Accuracy: Mide qué proporción de predicciones fueron correctas, tanto positivos, como negativos.

¿Cómo interpretar la matriz de confusión?
La matriz de confusión se interpreta por cada clase, la cantidad de Verdaderos positivos, falsos positivos (error de tipo I, no rechazo H0, pero H0 era falsa), verdaderos negativos,
falsos negativos (error de tipo II, rechazo H0, pero H0 era verdadera)

¿Cuándo usar accuracy vs otras métricas?
Considero que accuracy se utiliza solo cuando querés saber la cantidad de predicciones que hizo correctas el modelo y entiendo
que, cuando se quiere tener una perspectiva más real del rendimiento del modelo (teniendo en cuenta el total de casos que el modelo tuvo que analizar) o la proporción de qué tan balanceado está el modelo, podemos utilizar métricas como
precision, recall y f1-score.

Matriz de confusión: ¿En qué casos se equivoca más el modelo: cuando predice que una persona sobrevivió y no lo hizo, o al revés?
Según podemos visualizar en la Matriz de confusión, el modelo se equivoca más cuando predice que una persona no sobrevivió, pero en realidad sí lo hizo; esto ocurrió en
21 casos, vs 12 casos en los cuales una persona sí sobrevivió, pero el modelo predice que no lo hizo.

Clases atendidas: ¿El modelo acierta más con los que sobrevivieron o con los que no sobrevivieron?
El modelo acierta más con los que no sobrevivieron, esto debido a que tanto la precision como el recall son más altos en el grupo de los que no sobrevivieron.

Comparación con baseline: ¿La Regresión Logística obtiene más aciertos que el modelo que siempre predice la clase más común?
Sí, la Regresión Logística tuvo un 0.81 -> 81% de Accuracy (aciertos totales), frente al modelo que siempre predice la clase más común que tuvo un
0.61 -> 61% de Accuracy.

Errores más importantes: ¿Cuál de los dos tipos de error creés que es más grave para este problema?
Para este problema creo que es más grave el error de tipo II (falsos negativos), o sea, las personas que sí sobrevivieron, pero el modelo predijo que NO sobrevivieron,
esto lo considero debido a, por ejemplo, si este modelo se utilizara para sacar algún tipo de estadística de qué tan robusto era el Titanic.

Observaciones generales: Mirando las gráficas y números, ¿qué patrones interesantes encontraste sobre la supervivencia?
Encontré que la mayoría de supervivientes eran mujeres y niños (haciendo una breve investigación, me di cuenta que esto fue porque a la hora de asignar las balsas, este grupo de personas fue priorizado), también
que existía un patrón entre los supervivientes y la clase de su ticket, por lo que podemos entender que el nivel económico sí influía en este caso,
y por último pero no menos interesante, que la mayoría de sobrevivientes embarcaron en la puerta S = Southampton

Mejoras simples: ¿Qué nueva columna (feature) se te ocurre que podría ayudar a que el modelo acierte más?
Se me ocurre crear una feature que sea "SocioEconomical Level" que tenga 3 valores low, medium y high, y se calcule en base a verificar pclass (la clase del ticket del pasajero)
y fare (costo del ticket)
""""
## Evidencias
- Enlace a material o capturas en `docs/assets/`

## Reflexión
Lo más desafiante, lo más valioso, próximos pasos.

Considero que lo más desafiante fue aprender acerca de regresión Logistica, cómo funciona el modelo y cuándo aplicarlo, considero que es la base para luego
entender algunos modelos más complejos como árboles de decisión, redes neuronales, etc

También considero que fue vital aprender sobre las métricas de evaluación, ya que me hizo entender conceptos básicos a la hora de medir qué tan bien predice un modelo,
conceptos que entiendo que en la industria se miden automáticamente mediante una función, pero que considero que es necesario saber cómo funcionan por detrás, las fórmulas matemáticas que utilizan,
para así saber exactamente qué están midiendo, y cuándo es necesario realizar un ajuste.

## Próximos pasos:

Procedí a realizar un resumen para el IRAT de la unidad 1, y posteriormente realizar la tarea 4

