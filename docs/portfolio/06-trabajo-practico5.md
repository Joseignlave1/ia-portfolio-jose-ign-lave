---
title: "Entrada 06 — Clasificación y Validación de Modelos"
date: 2025-09-21
---

# Entrada 06 — Quinto trabajo práctico~~
~~

## Contexto
En este trabajo práctico exploramos técnicas avanzadas de clasificación y validación de modelos.  
Se utilizaron clasificadores lineales con regularización L2 (RidgeClassifier) y modelos de ensamble (RandomForestClassifier),  
junto con estrategias de validación cruzada como StratifiedKFold.  
Además, se profundizó en conceptos clave como clases balanceadas vs desbalanceadas, métricas de evaluación (accuracy, precision, recall, f1-score)  
y la importancia de evitar el data leakage mediante Pipelines.  
También se abordaron métodos de optimización de hiperparámetros (GridSearchCV y RandomizedSearchCV).  

## Objetivos
- Comprender el funcionamiento de RidgeClassifier y RandomForestClassifier.  
- Entender el concepto y la aplicación de técnicas de validación cruzada (cross_val_score, StratifiedKFold).  
- Identificar la diferencia entre clases balanceadas y desbalanceadas y su impacto en la evaluación.  
- Analizar la importancia de elegir métricas adecuadas (accuracy, precision, recall, f1-score).  
- Entender qué es data leakage y cómo evitarlo con Pipelines.  
- Entender el concepto de pipeline, y por qué es importante utilizarlo.  
- Implementar estrategias de optimización de hiperparámetros con GridSearchCV y RandomizedSearchCV.  
- Entender cómo se deciden la importancia de las variables en Random Forest.  
- Comprender el concepto de sesgo.  
- Entender cómo detectar sesgos en los modelos.  

## Actividades (con tiempos estimados)
- Investigación del dataset: tamaño, características y balance de clases — 15 min  
- Entender implementación paso a paso de RidgeClassifier y análisis de regularización L2 — 20 min  
- Entender entrenamiento paso a paso de RandomForestClassifier y revisión de cómo elige RandomForest las features importantes — 40 min  
- Entender paso a paso la validación cruzada con KFold y StratifiedKFold — 30 min  
- Entender la optimización de hiperparámetros con GridSearchCV y RandomizedSearchCV — 40 min  
- Responder las preguntas planteadas, investigando acerca de conceptos como data leakage y sesgos en modelos de clasificación — 30 min  

## Desarrollo
Comencé explorando el dataset de predicción de éxito estudiantil, verificando cuántas muestras y características incluía, así como el balance de las tres clases objetivo (Graduate, Enrolled y Dropout).  

A lo largo de la práctica, seguí paso a paso la implementación guiada que nos brindó el profesor, completando los espacios vacíos del código y entendiendo el rol de cada componente.  

Esto incluyó el RidgeClassifier con regularización L2, el RandomForestClassifier y cómo este último determina la importancia de las features.  

También repasé cómo funciona la validación cruzada, comparando KFold con StratifiedKFold, y entendí por qué este último es más adecuado en datasets desbalanceados.  

Más adelante, profundicé en la optimización de hiperparámetros con GridSearchCV y RandomizedSearchCV, comprendiendo sus diferencias y cuándo conviene aplicar cada técnica.  

Finalmente, respondí las preguntas de reflexión relacionadas con data leakage, la necesidad de usar Pipelines para evitarlo,  
y la importancia de la explicabilidad y detección de sesgos en modelos de clasificación,  
sobre todo en contextos sensibles como la educación o la medicina.  

Procedo a adjuntar las preguntas del trabajo práctico:  

IA I Tarea 5:  

Pistas:  
- RidgeClassifier: Documentación - Clasificador con regularización L2  
- RandomForestClassifier: Documentación - Ensemble de árboles de decisión  
- cross_val_score: Documentación - Para validación cruzada automática  
- StratifiedKFold: Documentación - KFold que mantiene proporción de clases  
- StandardScaler: Documentación - Estandariza características (media=0, std=1)  

### Preguntas para investigar  

- ¿Cuántas muestras y características tiene el dataset?  
  Tiene 4424 instancias (muestras) y 36 características (features).  

- ¿Qué tipos de variables incluye? (demográficas, académicas, socioeconómicas)  
  Incluye varios tipos:  
  - Demográficas: nacionalidad, estado civil, modalidad de aplicación.  
  - Académicas: calificación de la cualificación previa, tipo de cualificación anterior, camino académico.  
  - Socioeconómicas: nivel educativo de los padres, modalidad de aplicación específica.  
  - Además de variables categóricas y numéricas.  

- ¿Las clases están balanceadas o desbalanceadas?  
  No, están desbalanceadas:  
  - Graduate: 2209 (~50%)  
  - Dropout: 1421 (~32%)  
  - Enrolled: 794 (~18%)  

- ¿Qué significan las 3 categorías objetivo?  
  - Dropout: estudiantes que abandonan.  
  - Enrolled: estudiantes que siguen inscritos.  
  - Graduate: estudiantes que se gradúan.  

## Ridge Classifier con regularización L2
La regularización L2 es una técnica para evitar el sobreajuste (overfitting) en modelos de Machine Learning.  
Se agrega un término de penalización a la función de costo del modelo.  
A diferencia de L1 (Lasso), que lleva algunos coeficientes a 0, L2 los reduce en magnitud sin eliminarlos.  

Coeficientes = Pesos que el modelo le asigna a las features.  

## Random Forest
Random Forest no necesita StandardScaler porque hace divisiones por umbrales y no depende de la magnitud de las variables.  

## Métricas
- Accuracy: proporción de predicciones correctas sobre el total.  
- Precision: de todos los ejemplos que el modelo marcó como positivos, cuántos eran realmente positivos.  
- Recall: de todos los positivos reales, cuántos detectó el modelo.  
- F1-score: balance entre precision y recall.  

## Cross-validation
Es una técnica para evaluar la capacidad de un modelo de generalizar a datos nuevos.  
Consiste en dividir el dataset en varios subconjuntos (folds), entrenar el modelo con algunos y probarlo con los restantes, repitiendo el proceso varias veces.  

### BONUS: ¿Qué significan las métricas de validación?  

1. Cross-Validation: divide los datos en varias partes (folds) para entrenar y evaluar múltiples veces.  
2. Accuracy promedio: proporción de predicciones correctas promediada en todas las divisiones.  
3. Desviación estándar: indica qué tan estable es el modelo.  
4. StratifiedKFold: mantiene la proporción de clases en cada fold, útil en datasets desbalanceados.  

Un modelo estable tiene baja variabilidad.  
En medicina se prefiere un modelo consistente, ya que genera confianza en sus predicciones.  

## Optimización de hiperparámetros
- GridSearchCV: prueba todas las combinaciones posibles en la grilla (preciso pero lento).  
- RandomizedSearchCV: prueba combinaciones al azar (rápido pero no garantiza el óptimo).  

## Data leakage
Ocurre cuando información de validación/prueba se filtra al entrenamiento.  
Pipeline + SearchCV lo evitan porque cada transformación se ajusta solo con los datos de entrenamiento de cada fold, y luego se aplica al de validación.  

## Feature Importances en Random Forest
El atributo `.feature_importances_` mide cuánto reduce la impureza cada variable en promedio en todos los árboles.  
Si una feature contribuye mucho a separar bien las clases, tendrá mayor importancia.  

## Preguntas simples  

1. ¿Qué es data leakage y por qué es peligroso?  
   Data leakage es cuando ocurre una fuga de datos de validación hacia el modelo, lo que hace que parezca más preciso de lo que realmente es, impidiendo evaluar su verdadera capacidad de generalización.  

2. ¿Cuándo usar KFold vs StratifiedKFold?  
   Cuando las clases están balanceadas se puede usar KFold.  
   Cuando están desbalanceadas, conviene StratifiedKFold, ya que mantiene proporciones equitativas en cada fold.  

3. ¿Cómo interpretar "95.2% ± 2.1%" en cross-validation?  
   Significa que el modelo obtiene en promedio 95.2% de accuracy, con una variabilidad (desviación estándar) de ±2.1% entre los folds.  

4. ¿Por qué Random Forest no necesita StandardScaler?  
   Porque trabaja con divisiones por umbrales y no depende de la magnitud de las variables.  

5. En diagnóstico médico, ¿prefieres un modelo con 98% accuracy pero inestable, o 95% accuracy pero muy estable?  
   Prefiero un modelo con 95% de accuracy pero muy estable, ya que garantiza predicciones consistentes y confiables, lo cual es esencial en medicina.  

## Evidencias
https://colab.research.google.com/drive/1-FtzjbWMymjJyy42tHkszzyLcHcm7Zt3?usp=sharing  

## Reflexión  
Mediante este trabajo, pude aprender el concepto y uso de varios classifiers,  
y entender en qué situaciones conviene utilizar cada uno.  

También comprendí la importancia de evitar el data leakage,  
qué significa este problema y cómo puede afectar la evaluación del modelo.  

Por último, pude afianzar el concepto de cross-validation,  
y entender por qué es una técnica tan útil para medir qué tan bien generaliza el modelo ante datos nuevos,  
entendiendo los dos tipos de approaches: KFold y StratifiedKFold, y cuándo utilizar cada uno.  

## Próximos pasos
Procedí a realizar la tarea 6
