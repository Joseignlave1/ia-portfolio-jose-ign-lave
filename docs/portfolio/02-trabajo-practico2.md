---
title: "Entrada 02 — Primer Trabajo Práctico"
date: 2025-01-01
---

# Entrada 02 — Práctico 1: EDA del Titanic en Google Colab

## Contexto
Trabajamos con el dataset del Titanic, el cual contiene información sobre un conjunto de pasajeros. La idea era familiarizarnos con el uso de Google Colab, Python, y los métodos de la biblioteca de scikit-learn, la cual provee métodos para entrenar modelos de machine learning.

## Objetivos
•Familiarizarme con la sintaxis de Python.  
•Familiarizarme con la sintaxis de scikit-learn.  
•Poder visualizar los datos.  
•Poder darme cuenta de una correlación entre ciertos atributos y el hecho de que una persona haya sobrevivido.  

## Actividades (con tiempos estimados)
•Investigación del Dataset del Titanic (10 minutos).  
•Setup en Colab (5 min).  
•Cargar el dataset de Kaggle (2 opciones) (5-10 min).  
•Conocer el dataset (10 min).  
•EDA visual con seaborn/matplotlib (15 min).  

## Desarrollo
Primero se procedió a realizar la investigación del dataset, para ello procedí a responder las preguntas planteadas por el profesor.  

También revisé notebooks públicos, en específico los de:  
https://www.kaggle.com/code/alexisbcook/titanic-tutorial  
https://www.kaggle.com/code/yousefaymanatia/titanic-predictions  

Los cuales me ayudaron a entender mejor el funcionamiento de Kaggle, así como la sintaxis de la biblioteca de scikit-learn y que había una fuerte correlación entre el sexo de los pasajeros y si sobrevivieron. Se podía ver que más de un 75% de mujeres sobrevivieron, frente a un 18% de hombres. Esto, según investigué, fue debido a que en el Titanic se priorizaron los botes salvavidas primero a las mujeres y niños, y luego a los hombres.  

Luego procedí a investigar acerca de Google Colab, ya que era una herramienta con la cual no estaba familiarizado. Posteriormente ejecuté la primera parte del código brindado por el docente, lo que me permitió aprender acerca de diferentes métodos (.shape, .head, .info, .describe, etc).  

Por último realicé una visualización de los datos utilizando seaborn y matplotlib, pudiendo visualizar los datos en distintos tipos de gráficas (countplots, barplot, histplot, heatmap, etc).  

Procedo a adjuntar las preguntas del práctico.

"""
IA I Práctico I

Investigación del Dataset del Titanic

Preguntas:

1- ¿De qué trata exactamente este dataset?  
Este dataset trata de pasajeros del Titanic, se divide en 2 grupos: train.csv y test.csv.  
train.csv va a ser el dataset que debemos utilizar para entrenar a nuestro modelo, este contiene detalles de un subconjunto de pasajeros (891) en los cuales se revela si sobrevivieron o no al Titanic.  
test.csv contiene información similar, pero no revela si sobrevivieron o no.  

2- ¿Cuál es el objetivo de la competencia de Kaggle?  
El objetivo de la competencia es, utilizando machine learning, crear un modelo que prediga cuáles pasajeros sobrevivieron al Titanic.  

3- ¿Qué columnas/atributos contiene el dataset?  
El dataset contiene las siguientes columnas:  
survival — Survival — 0 = No, 1 = Yes  
pclass — Ticket class — 1 = 1st, 2 = 2nd, 3 = 3rd  
sex — Sex  
age — Age in years  
sibsp — # of siblings / spouses aboard the Titanic  
parch — # of parents / children aboard the Titanic  
ticket — Ticket number  
fare — Passenger fare  
cabin — Cabin number  
embarked — Port of Embarkation — C = Cherbourg, Q = Queenstown, S = Southampton  

4- ¿Qué representa cada una?  
survival = representa si el pasajero sobrevivió o no al Titanic — 0 = No, 1 = Yes  
pclass = Clase de su boleto (de acá se puede inferir posición económica).  
sex = Sexo, entiendo que hombre o mujer.  
sibsp = Número de hermanos / cónyuges a bordo.  
parch = Número de padres / hijos a bordo.  
ticket = Número de ticket.  
fare = Tarifa del pasajero.  
cabin = Número de cabina.  
embarked = Puerto de embarque (C = Cherbourg, Q = Queenstown, S = Southampton).  

5- ¿Cuál es la variable objetivo?  
Entiendo, según estuve investigando, que la variable objetivo es la variable que representa el resultado de lo que queremos predecir.  
Por lo tanto, como queremos predecir cuáles pasajeros sobrevivieron o no al Titanic, en este caso nuestra variable objetivo sería `survival`.  
Las demás variables serían predictoras o explicativas.  

6- Notebooks públicos revisados:  
https://www.kaggle.com/code/alexisbcook/titanic-tutorial  
https://www.kaggle.com/code/yousefaymanatia/titanic-predictions  

7- ¿Qué factores crees que más influyeron en la supervivencia?  
Considero que los factores que más influyeron en la supervivencia fueron el sexo y la puerta de embarque, ya que se pudo ver en los notebooks que más de un 75% de mujeres sobrevivieron frente a un 18% de hombres y que la gran mayoría de supervivientes provenían de la puerta de embarque S = Southampton.  

train_data[train_data["Survived"] == 1]["Embarked"].value_counts()  
Embarked  
S    217  
C     93  
Q     30  
Name: count, dtype: int64  

8- ¿Qué desafíos de calidad de datos esperas encontrar?  
Los desafíos de calidad que espero encontrar son:  
Age = el hecho de que sea un decimal, aunque entiendo que se hace así por la edad de los menores de 1 año.  
Cabin = muchas son NaN.  
Ticket = formato inconsistente, algunas filas tienen números y strings, y otras solo strings.  

9- ¿Qué variables podrían estar correlacionadas?  
Considero que las variables `fare` y `pclass` sin duda están relacionadas, ya que la clase asignada está correlacionada con el precio de tu boleto.  
Entiendo que `cabin` con `pclass` también está relacionada, ya que supongo que solo los que pagaron primera clase tienen una cabina.  

Preguntas finales:  
¿Qué variables parecen más relacionadas con Survived?  
Considero que las variables más relacionadas con Survived basándonos en el mapa de calor de correlaciones y en los otros gráficos son:  

fare = podemos visualizar que a mayor tarifa tenía el pasajero, más probable era que sobreviviera.  

sex = ya que podemos visualizar, mediante el notebook de https://www.kaggle.com/code/alexisbcook/titanic-tutorial, que más de un 75% de mujeres sobrevivieron, frente a un 18% de hombres.  

¿Dónde hay más valores faltantes? ¿Cómo los imputarías?  
Considero que hay más valores faltantes en la columna "cabin", ya que entiendo que solo los pasajeros de primera clase tenían una cabina asignada. Una buena técnica para imputarlos sería asignarle el valor de "None" a los registros que no tengan cabina.  

¿Qué hipótesis probarías a continuación?  
La hipótesis que probaría sería el hecho de que a mayor tarifa, más probable es que el pasajero sobreviva, por lo que podemos inferir que el nivel socioeconómico de los pasajeros está estrechamente relacionado. También probaría el hecho de que si eras mujer era mucho más probable que sobrevivieras.  
Investigando el porqué de este suceso, descubrí que en el Titanic se aplicó una política de "women and children first", por lo que mujeres y niños tenían prioridad para ocupar los botes salvavidas, lo que explica la gran diferencia de porcentajes.  
""""

## Evidencias
https://github.com/Joseignlave1/IA1-Practico-1  
https://colab.research.google.com/drive/15o-YyiTofFsIXhvJsMzP_2webeBdO2fq#scrollTo=cCqPtd1qDe_e  

## Reflexión
Considero que lo más desafiante en este caso fue familiarizarme con la biblioteca de scikit-learn y con las competencias de Kaggle.  
En mi caso personal no tenía idea de machine learning en general ni de qué se trataba Kaggle. Me inscribí a esta materia debido a que cursé Probabilidad y Estadística el semestre pasado, y como me gustó tanto, desembocó en un interés por el machine learning.  

A su vez pude empezar a entender los conceptos de "dataset", "atributos", y técnicas para "imputar" valores faltantes en un dataset.  

## Próximos pasos
Lo próximo que hice, debido a que me inscribí tarde a la materia, fue directamente continuar con la realización de la práctica 2, en la cual pude empezar a entender cómo funciona un modelo de **Regresión Logística**, qué es un **Dummy Classifier**, qué significa el concepto de métricas de evaluación y cuáles son las principales que debería tener en cuenta para medir qué tan bien predice un modelo.  
