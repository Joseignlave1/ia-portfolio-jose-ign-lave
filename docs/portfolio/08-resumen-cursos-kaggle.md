---
title: "Entrada 07 — Construcción y Evaluación de Modelos"
date: 2025-09-21
---

# Entrada 07 — Resumen de curso Kaggle~~
~~

## Contexto
En esta práctica repasamos los pasos principales para **construir, entrenar y evaluar modelos de Machine Learning**, siguiendo la metodología **CRISP-DM**.  
Se trabajó con librerías como **pandas**, **numpy** y **scikit-learn**, aplicando técnicas de preparación de datos, imputación de valores faltantes, preprocesamiento de variables categóricas, validación y evaluación de modelos.  

## Objetivos
- Comprender el concepto de “un modelo” en Machine Learning.  
- Familiarizarse con el proceso **CRISP-DM**.  
- Practicar con pandas y numpy en la exploración de datos.  
- Construir y evaluar un modelo de regresión de árboles de decisión.  
- Entender métricas de clasificación y regresión (MAE, Accuracy, Precision, Recall, F1, MSE, Log-Loss).  
- Aplicar técnicas de limpieza de datos y preprocesamiento de variables categóricas.  
- Introducir el concepto de **pipelines** y validación cruzada.  
- Revisar métodos avanzados como **Gradient Boosting** y prevenir problemas como el **data leakage**.  

---

## Un modelo y CRISP-DM
Un **modelo** es una representación matemática que aprende patrones de los datos para predecir un resultado.  
El flujo de trabajo sigue **CRISP-DM**:  
![CRISP-DM](assets/image1.png)

---
## Métodos de pandas y exploración de datos
- `import pandas as pd`: importar pandas.  
- `pd.read_csv("ruta")`: leer datos desde un CSV.  
- `train.head()`: primeras filas (por defecto 5).  
- `train.info()`: información del dataset.  
- `train.columns`: nombres de las columnas.  
- `train.dropna(axis=0)`: eliminar filas con valores vacíos.  
- `train.describe()`: estadísticas descriptivas.  

![EDA](assets/image2.png)  
![EDA_NaN](assets/image3.png)  
![EDA_Survived](assets/image4.png)  
![EDA_Extra](assets/image5.png)  
![EDA_Extra2](assets/image6.png)  

---
## Construcción de un modelo

### Definir target y features
`y = melbourne_data.Price`  
`melbourne_features = ['Rooms','Bathroom','Landsize','Lattitude','Longtitude']`  
`X = melbourne_data[melbourne_features]`  

### Pasos para construir un modelo
![PasosModelo](assets/image7.png)

### Definir y entrenar el modelo
from sklearn.tree import DecisionTreeRegressor  
melbourne_model = DecisionTreeRegressor(random_state=1)  
melbourne_model.fit(X, y)  

### Hacer predicciones
print("Making predictions for the following 5 houses:")  
print(X.head())  
print("The predictions are")  
print(melbourne_model.predict(X.head()))  

### Evaluar con MAE
**Mean Absolute Error (MAE):** mide en promedio cuánto se alejan las predicciones de los valores reales.  
![MAE](assets/image8.png)

---
## Train/Test Split y Overfitting

Separar los datos de entrenamiento y validación permite evaluar correctamente el modelo,  
ya que si solo usamos los datos de entrenamiento podríamos sobreestimar su rendimiento.

El **overfitting** ocurre cuando el modelo memoriza demasiado los datos de entrenamiento  
y pierde capacidad de generalizar en datos nuevos.

![Split](assets/image9.png)  
![Overfitting](assets/image10.png)

Ejemplo de comparación de errores según cantidad de hojas en el árbol:

for max_leaf_nodes in [5, 50, 500, 5000]:  
    my_mae = get_mae(max_leaf_nodes, train_X, val_X, train_y, val_y)  
    print("Max leaf nodes:", max_leaf_nodes, "   Mean Absolute Error:", my_mae)

---

## EDA Visualizaciones
Durante la exploración de datos podemos visualizar distribuciones, valores faltantes y relaciones entre variables.  

![EDA_Visual1](assets/image11.png)  
![EDA_Visual2](assets/image12.png)  
![EDA_Visual3](assets/image13.png)  

---

## Manejo de valores faltantes

![MissingValues](assets/image14.png)  

Existen varias técnicas para manejar valores faltantes en un dataset:

1. **Drop Columns with Missing Values**  
   Consiste en eliminar filas o columnas con datos faltantes.  
   ⚠️ No recomendado porque puede eliminar información valiosa.  

   ![DropExample](assets/image37.png)  
   ![DropExample2](assets/image38.png)  

2. **Imputation**  
   Se rellenan los valores faltantes con la media, mediana o moda.  
   Por defecto, `SimpleImputer()` usa la mediana.  

   ![Imputation](assets/image39.png)  
   ![ImputationStrategies](assets/image40.png)  
   ![ImputationExample](assets/image41.png)  
   ![Strategies](assets/image42.png)  

3. **Extension to Imputation**  
   Además de imputar, se crea una columna booleana que marca si un valor fue imputado (TRUE/FALSE).  
   Esto permite al modelo saber dónde había datos faltantes.  

   ![Extension](assets/image43.png)  
   ![ExtensionExample](assets/image44.png)  

---
## Variables Categóricas

Las variables categóricas son aquellas que toman un valor dentro de un conjunto definido y finito de posibilidades.  
Ejemplo: frecuencia de almuerzo → “never”, “rarely”, “most days”, “every day”.  

Antes de usarlas en un modelo de Machine Learning, deben **preprocesarse**.  

Para identificarlas podemos filtrar las columnas con tipo de dato `object` (strings).  

![ObjectColumns](assets/image45.png)  

---

## Técnicas de preprocesamiento de variables categóricas

1. **Drop Categorical Variables**  
   Eliminar columnas categóricas que no aportan información útil.  
   ![DropCategorical](assets/image46.png)  
   Ejemplo:  
   ![DropExample](assets/image47.png)  

2. **Ordinal Encoding**  
   Convierte las categorías en números enteros, asumiendo un orden lógico.  
   ![OrdinalEncoding](assets/image48.png)  
   Ejemplo:  
   ![OrdinalExample](assets/image49.png)  

3. **One-Hot Encoding**  
   Crea nuevas columnas binarias (0/1) para cada categoría, sin asumir un orden.  
   Útil para categorías nominales.  
   ⚠️ No recomendable cuando hay muchas categorías (>15), ya que aumenta exponencialmente las columnas.  
   ![OneHot](assets/image50.png)  
   Ejemplo:  
   ![OneHotExample1](assets/image51.png)  
   ![OneHotExample2](assets/image52.png)  

---
## Pipelines

Un **Pipeline** permite empaquetar todos los pasos de construcción de un modelo  
(entrenamiento, transformaciones y predicciones) en un solo objeto.  
Esto facilita la ejecución y el mantenimiento, además de evitar fugas de datos (**data leakage**).  

![Pipeline](assets/image53.png)  

Ejemplo de pipeline con RandomForest:  
![PipelineSteps](assets/image54.png)  
![PipelineDetail](assets/image55.png)  
![PipelineRF1](assets/image56.png)  
![PipelineRF2](assets/image57.png)  

---

## Cross-Validation

La **validación cruzada (cross-validation)** consiste en dividir el dataset en *k* partes (folds).  
El modelo se entrena con *k-1* folds y se valida con el fold restante, repitiendo el proceso *k* veces.  
El rendimiento final es el promedio de los resultados en cada fold.  

Ventaja: proporciona una estimación más robusta de la capacidad de generalización del modelo.  

![CV](assets/image58.png)  

Ejemplo con k=5:  
- Cada fold tiene el 20% de los datos.  
- Se realizan 5 experimentos.  
- Cada fold actúa una vez como validación.  
- El resultado final es el promedio de los 5 scores.  

¿Cuándo usarlo?  
- **Datasets pequeños** → conviene usar cross-validation.  
- **Datasets grandes** → single validation es suficiente (ahorra recursos).  

![CVExample1](assets/image59.png)  
![CVExample2](assets/image60.png)  
![CVExample3](assets/image61.png)  
![CVExample4](assets/image62.png)  

---
## Gradient Boosting

El **Gradient Boosting** es un método de ensamble: combina múltiples modelos débiles  
(árboles de decisión simples) para construir un modelo más fuerte.  

El proceso:  
1. Se entrena un modelo sencillo.  
2. Se calculan los errores (pérdida, por ejemplo con MSE).  
3. Se entrena un nuevo modelo para corregir los errores del anterior.  
4. Los modelos se combinan sumando sus predicciones.  
5. El ciclo se repite varias veces.  

![GB](assets/image63.png)  

---

## Parámetros principales

- **n_estimators**  
  Número de modelos que se entrenan en el ciclo.  
  - Muy bajo → underfitting.  
  - Muy alto → overfitting.  

- **early_stopping_rounds**  
  Detiene el entrenamiento cuando la métrica de validación deja de mejorar.  
  Permite encontrar automáticamente el número óptimo de iteraciones.  

- **learning_rate**  
  Escala las predicciones de cada modelo antes de combinarlas.  
  Valores bajos → entrenamiento más lento pero más preciso.  

- **n_jobs**  
  Permite usar varios núcleos del procesador en paralelo para acelerar el entrenamiento.  

![GB_Params1](assets/image64.png)  
![GB_Params2](assets/image65.png)  

---
## Data Leakage

El **Data Leakage** ocurre cuando el modelo accede a información del target (variable a predecir)  
que no estará disponible en producción.  
Esto genera resultados artificialmente buenos en validación, pero inútiles en el mundo real.  

---

### Target Leakage
Sucede cuando ciertas variables contienen información que solo se conoce después del evento que se quiere predecir.  
Ejemplo: usar el campo `took_antibiotic_medicine` para predecir neumonía.  
Ese dato solo se conoce tras el diagnóstico, no antes.  

![TargetLeakage1](assets/image66.png)  
![TargetLeakage2](assets/image67.png)  
![TargetLeakage3](assets/image68.png)  

---

### Train-Test Contamination
Ocurre cuando datos del conjunto de validación se filtran en el entrenamiento,  
ya sea por una mala división de los datos o por aplicar transformaciones antes del split.  

![Contamination1](assets/image69.png)  
![Contamination2](assets/image70.png)  

**Cómo evitarlo:**  
- Dividir primero en train y test, y recién después aplicar transformaciones.  
- Usar **pipelines**, ya que se ajustan solo con datos de entrenamiento en cada fold.  

![ContaminationFix](assets/image71.png)  

---

## Ejemplo de competencia (Kaggle)
[Home Data for ML Course](https://www.kaggle.com/c/home-data-for-ml-course)  

---
## Métricas de Clasificación y Regresión

Las métricas permiten evaluar qué tan bien performa un modelo.  

---

### Accuracy
Proporción de predicciones correctas (positivas y negativas) sobre el total.  
![Accuracy](assets/image22.png)  

---

### Precision
De todos los casos que el modelo predijo como positivos, ¿cuántos realmente lo eran?  
![Precision](assets/image23.png)  

---

### Recall
De todos los casos positivos reales, ¿cuántos identificó correctamente el modelo?  
![Recall](assets/image24.png)  

---

### F1-score
Promedio armónico entre *precision* y *recall*.  
Mide qué tan balanceado está el modelo entre ambas métricas.  
Siempre da un valor entre 0 y 1.  
![F1](assets/image25.png)  

---

## Métricas en Regresión

Cuando queremos predecir valores numéricos (ejemplo: precio de una casa).  

### Mean Absolute Error (MAE)
Promedio de los errores absolutos entre predicciones y valores reales.  
Ya visto en la construcción del modelo.  

### Mean Squared Error (MSE)
Promedio de los errores al cuadrado. Penaliza más los errores grandes.  
![MSE](assets/image31.png)  

---

## Regresión Lineal
El modelo predice valores continuos.  
- Y = output (predicción).  
- X = features.  
- W = coeficientes (peso de cada feature).  
- B = bias.  

![Linear1](assets/image28.png)  
![Linear2](assets/image29.png)  
![Linear3](assets/image30.png)  

---

## Regresión Logística
Se utiliza para clasificación binaria (0/1).  
El output es una probabilidad entre 0 y 1.  
- Si P ≥ 0.5 → predice 1 (Sí).  
- Si P < 0.5 → predice 0 (No).  

![Logistic1](assets/image32.png)  
![Logistic2](assets/image33.png)  
![Logistic3](assets/image34.png)  

### Cross-Entropy (Log-Loss)
Métrica para evaluar clasificación probabilística.  
Mide qué tan bien la probabilidad predicha se acerca a la clasificación real.  
![LogLoss](assets/image35.png)  
![LogLossDiff](assets/image36.png)  

---

## Comparación final
- **Regresión Lineal + MSE** → predicciones de valores continuos.  
- **Regresión Logística + Log-Loss** → clasificación binaria probabilística.  

---
## Reflexión Final:
Pude aprender acerca de los conceptos del curso, realizando un resumen de los contenidos del curso

## Proximos pasos:
Voy a proceder a hacer los desafíos de kaggle para asi poder afianzar mis conocimientos en Machine Learning.