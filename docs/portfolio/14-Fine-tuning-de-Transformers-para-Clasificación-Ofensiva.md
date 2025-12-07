---
title: "Entrada 14 — UT4 Clasificación de Sentimiento Financiero con TF-IDF y Transformers"
date: 2025-11-10
---

# Entrada 14 — Fine-tuning-de-Transformers-para-Clasificación-Ofensiva
~~

## Contexto
En este trabajo práctico trabajamos con técnicas modernas de **procesamiento de lenguaje natural (NLP)** aplicadas al análisis de sentimiento financiero.  
El objetivo fue comparar un enfoque clásico basado en **TF-IDF + Logistic Regression** con un modelo Transformer de última generación  
fine-tuneado sobre un dataset de tweets financieros en inglés.

El dataset utilizado fue:  
**zeroshot/twitter-financial-news-sentiment**, un conjunto de ~12k ejemplos con tres clases de sentimiento:  
**Bearish (0), Bullish (1), Neutral (2)**.  

Este trabajo aborda el flujo completo de NLP moderno:  
carga de datos → exploración visual → baselines clásicos → fine-tuning con Transformers → comparación de performance.

## Objetivos
- Cargar y preprocesar datasets de texto utilizando Hugging Face Datasets.  
- Normalizar datos en DataFrames y preparar splits estratificados.  
- Aplicar análisis exploratorio de texto: longitudes, distribución de clases, n-grams, TF-IDF, UMAP/PCA y Word2Vec.  
- Implementar un baseline clásico con **TF-IDF + Logistic Regression**.  
- Entrenar un modelo Transformer (FinBERT u otro checkpoint) con fine-tuning.  
- Comparar performance entre Bag-of-Words y Transformers usando accuracy y macro-F1.  
- Reflexionar sobre trade-offs entre modelos clásicos vs. modelos modernos.  

## Actividades (con tiempos estimados)
- Carga y normalización del dataset — 20 min  
- Exploración de longitudes, distribución de clases y n-grams — 25 min  
- Visualizaciones con TF-IDF, PCA/UMAP y Word2Vec — 30 min  
- Implementación del baseline TF-IDF + Logistic Regression — 20 min  
- Fine-tuning de un Transformer (FinBERT) — 45 min  
- Evaluación y comparación final — 20 min  
- Responder preguntas teóricas y análisis de resultados — 25 min  

## Desarrollo
Comencé cargando el dataset desde Hugging Face Datasets y creé una función de normalización  
para estandarizar todas las columnas a un DataFrame con `text` y `label`.  
Esto permitió trabajar con un pipeline unificado durante todo el trabajo.

Luego realicé un análisis exploratorio inicial:  
- distribución de longitudes del texto,  
- distribución de clases,  
- identificación de posibles desbalances,  
- extracción de n-grams por clase,  
- generación de nubes de palabras.  

Más adelante incorporé un EDA más profundo utilizando **TF-IDF combinado con PCA y UMAP**,  
lo cual ayudó a evaluar si las clases tenían separabilidad natural en el espacio vectorial.  
También entrené un modelo pequeño de **Word2Vec** para observar vecinos semánticos en vocabulario financiero.

Después implementé el baseline clásico utilizando **TF-IDF + Logistic Regression**,  
que sirvió como punto de comparación para medir cuánto aporta realmente el fine-tuning con Transformers.

La parte central del trabajo fue entrenar un modelo Transformer, evaluando distintas opciones de checkpoints.  
Finalmente, comparé resultados entre ambos enfoques utilizando accuracy y macro-F1,  
junto con la matriz de confusión para entender errores comunes.

## Evidencias
https://colab.research.google.com/drive/1Jvj0kuusA0bRNjjYHHBBiOKhuuvMSUV7#scrollTo=eQBsjN-RN9Gf

## Reflexión
Este trabajo me permitió ver con claridad las diferencias prácticas entre un enfoque clásico basado en Bag-of-Words  
y un modelo preentrenado tipo Transformer. A continuación respondo las preguntas de reflexión solicitadas:

### 1. Distribución de longitudes  
Observé que los textos eran relativamente cortos (tweets), con longitudes variables pero manejables.  
Esto implica que el **tokenizer debe utilizar truncation**, ya que algunos ejemplos superaban la longitud estándar del modelo.  
También indica que no es necesario usar ventanas muy largas y que la semántica relevante está concentrada.

### 2. Desbalance de clases  
Las clases estaban **moderadamente desbalanceadas**, con predominancia de la clase Neutral.  
Esto afecta las métricas, ya que un modelo puede obtener buena accuracy priorizando esa clase.  
Por eso utilicé **macro-F1**, que distribuye el peso equitativamente entre clases.

### 3. N-grams y WordClouds  
En los n-grams más frecuentes aparecieron términos específicos del dominio financiero,  
como movimientos de mercado, tickers y opiniones cortas típicas de Twitter.  
En las WordClouds se observó bastante ruido propio de redes sociales: abreviaturas, hashtags, emojis y expresiones coloquiales.

### 4. Separabilidad en PCA/UMAP  
En la proyección con PCA la separabilidad fue baja, lo cual es esperable en texto corto.  
UMAP mostró algo más de estructura, especialmente para los extremos Bearish/Bullish,  
pero las clases seguían solapadas, reflejando ambigüedad inherente del lenguaje financiero.

### 5. Baseline TF-IDF + Logistic Regression  
El baseline funcionó razonablemente bien y capturó patrones léxicos simples,  
pero falló especialmente en los casos ambiguos o frases con ironía.  
TF-IDF depende exclusivamente de la superficie del texto, sin utilizar contexto.

### 6. Fine-tuning con Transformers  
El modelo Transformer (FinBERT) **superó ampliamente** al baseline en macro-F1 y en estabilidad entre clases.  
Esto se debe a que incorpora conocimiento contextual preentrenado en dominio financiero,  
capaz de interpretar relaciones semánticas incluso en textos cortos.

### 7. Costos de entrenamiento  
El entrenamiento del Transformer requirió más tiempo y memoria GPU,  
pero se mantuvo dentro de límites razonables en Colab, especialmente usando batch sizes moderados.  
El costo computacional fue mayor, pero también los beneficios.

### 8. Comparación final  
El Transformer mostró:  
- mejor manejo de oraciones ambiguas,  
- mejor generalización,  
- mucho mejor macro-F1,  
- menos sesgo hacia la clase mayoritaria.  

El baseline, sin embargo, sigue siendo útil por su **simplicidad, velocidad y facilidad de despliegue**.

### 9. ¿Qué modelo elegiría para producción?  
En un entorno financiero donde el costo del error es alto, elegiría el **Transformer**,  
ya que captura matices semánticos imprescindibles para interpretar sentimiento.  
El baseline es útil como sistema rápido o backup liviano.

### 10. Mejoras futuras  
Si continuara este trabajo, exploraría:  
- **limpieza de datos y normalización de textos** para reducir ruido,  
- **weighted loss o focal loss** para compensar clases minoritarias,  
- probar RAG o modelos más grandes,  
- incorporar **aumentación textual** (EDA, back-translation),  
- evaluación del modelo con datos reales de mercado.

## Próximos pasos
Procedí a realizar la tarea de la UT4 LLMs con LangChain (OpenAI) — Prompting, Plantillas y Salida Estructurada
