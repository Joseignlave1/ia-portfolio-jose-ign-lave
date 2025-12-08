---
title: "Entrada Extra — Clasificación con el Dataset IRIS"
date: 2025-09-21
---

# Entrada Extra — Regresion Lineal y Regresion Logistica IRIS

## Contexto
En esta actividad trabajamos con uno de los datasets más clásicos y utilizados en machine learning supervisado: **IRIS**, que contiene mediciones de flores pertenecientes a tres especies diferentes. El objetivo es desarrollar un modelo de clasificación capaz de predecir correctamente la especie de cada flor en función de cuatro características morfológicas. Esta tarea permitió reforzar los conceptos de modelos lineales, preprocesamiento y métricas de evaluación para clasificación multiclase.

## Objetivos
- Comprender la estructura del dataset IRIS y la naturaleza multiclase de su problema.
- Implementar un modelo de clasificación supervisada utilizando `LogisticRegression`.
- Entrenar y evaluar el modelo siguiendo buenas prácticas (train/test split).
- Analizar el rendimiento del modelo utilizando métricas de clasificación multiclase.
- Desarrollar criterio para interpretar probabilidades, predicciones y errores del modelo.

## Actividades (con tiempos estimados)
- Exploración inicial del dataset IRIS — 15 min  
- Preprocesamiento: selección de features y revisión de la variable objetivo — 10 min  
- División en entrenamiento y prueba — 10 min  
- Entrenamiento del modelo con regresión logística multiclase — 30 min  
- Evaluación con accuracy, matriz de confusión y reporte de clasificación — 30 min  
- Respuesta a preguntas de reflexión — 25 min  

## Desarrollo
Comencé explorando el dataset IRIS para identificar las variables disponibles: largo y ancho del sépalo, largo y ancho del pétalo y la especie correspondiente a cada observación.  
La variable objetivo contiene tres clases (`setosa`, `versicolor`, `virginica`), lo cual convierte el ejercicio en un problema de **clasificación multiclase**.

Luego realicé un repaso del funcionamiento de la regresión logística en escenarios donde el modelo debe asignar probabilidades a más de dos categorías. En estos casos se utiliza una función softmax para obtener probabilidades que suman uno entre todas las clases.

Seguí la consigna implementando paso a paso el modelo de regresión logística con `scikit-learn`, ajustando `max_iter` para asegurar la convergencia. A medida que avanzaba, anoté funciones que no recordaba, como `classification_report` y `confusion_matrix`.

Finalmente, realicé las evaluaciones solicitadas y respondí las preguntas de reflexión.

### Caso de negocio
* Problema: Un botánico desea clasificar automáticamente flores recolectadas en campo.  
* Objetivo: Predecir la especie basada en características físicas observables.  
* Variables: Largo/ancho de sépalo y pétalo.  
* Valor: Automatizar catalogación, disminuir errores humanos y acelerar el registro de especies.  

---

### Preguntas guía y recordatorio de sklearn

* Clase utilizada: `LogisticRegression` con `multi_class='auto'` (por defecto).  
* División de datos: `train_test_split`.  
* Entrenamiento: `.fit()`.  
* Predicción: `.predict()`.  

Métricas utilizadas:  
* `accuracy_score`  
* `confusion_matrix`  
* `classification_report`  

Interpretación de métricas:
1. **Accuracy:** porcentaje total de aciertos.  
2. **Precision:** de los predichos para una clase, cuántos eran correctos.  
3. **Recall:** de los ejemplos reales de una clase, cuántos se detectaron.  
4. **F1-score:** balance entre precision y recall.  
5. **Matriz de Confusión:** muestra cómo se distribuyen aciertos y errores entre clases.

---

### Preguntas de Reflexión

1. **¿Por qué este problema no puede resolverse con regresión lineal?**  
Porque la regresión lineal predice valores continuos y no categorías. El dataset IRIS requiere asignar un ejemplo a una de tres clases discretas, lo cual es propio de un modelo de clasificación.

2. **¿Por qué es necesario usar softmax en problemas multiclase?**  
Porque softmax convierte los logits en probabilidades que suman 1, permitiendo que el modelo distribuya la probabilidad entre múltiples categorías y elija la más probable.

3. **¿Qué significaría un accuracy del 97% en este contexto?**  
Significa que el modelo clasificó correctamente el 97% de las flores. En un conjunto de 100 flores, acertó 97.

4. **¿Qué clase suele ser más fácil de predecir en IRIS y por qué?**  
`setosa` suele ser la más fácil porque sus características (en especial el tamaño del pétalo) están muy separadas del resto, lo cual facilita su identificación por parte del modelo.

---

## Evidencias
https://colab.research.google.com/drive/1ewO703qG6N14EpXwI_BGrZm4z__EaP9X?authuser=0#scrollTo=v2SH1b1__WnW

## Reflexión
Este ejercicio me permitió afianzar el uso práctico de la regresión logística en escenarios más complejos que la clasificación binaria clásica. Trabajar con tres clases me obligó a interpretar mejor la matriz de confusión y los reportes por clase.  

Además, reforcé la idea de que el preprocesamiento y la correcta división del dataset siguen siendo fundamentales para evitar overfitting. Al comparar el rendimiento del modelo en train y test, pude revisar posibles desviaciones o errores sistemáticos.

También entendí la importancia de la interpretación de softmax en modelos multiclase y cómo esto afecta la selección final de la categoría. El trabajo profundizó mi comprensión de cómo los modelos lineales pueden adaptarse a distintos tipos de problemas según la naturaleza de la variable objetivo.

## Próximos pasos
Proceder con la implementación de modelos más avanzados para clasificación multiclase (Árboles, Random Forest, SVM) y comparar su rendimiento con la regresión logística para distintos tipos de datasets.
