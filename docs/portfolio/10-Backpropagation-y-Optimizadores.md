---
title: "Entrada 10 — Backpropagation y Optimizadores"
date: 2025-10-12
---

# Entrada 10 — Backpropagation y Optimizadores~~
~~

## Contexto
En esta práctica trabajamos el concepto de **backpropagation** y el rol de los **optimizadores** dentro del entrenamiento de redes neuronales.  
El objetivo principal fue entender cómo se ajustan los pesos a partir del error que comete el modelo y cómo distintos algoritmos de optimización impactan en la convergencia y precisión final.  
El trabajo se realizó utilizando **TensorFlow/Keras** sobre el dataset **CIFAR-10**, compuesto por 60.000 imágenes en 10 categorías, lo que permitió aplicar redes neuronales densas (MLP) y observar sus limitaciones frente a datos visuales.

## Objetivos
- Comprender el proceso de backpropagation y su importancia en el aprendizaje del modelo.  
- Implementar una red neuronal multicapa (MLP) con TensorFlow/Keras.  
- Explorar distintos optimizadores como Adam, SGD y RMSprop.  
- Analizar la influencia de hiperparámetros como learning rate, batch size y epochs.  
- Evaluar la performance mediante accuracy y loss utilizando TensorBoard.  

## Actividades (con tiempos estimados)
- Preparación del entorno y carga de librerías — 10 min  
- Carga, normalización y división del dataset CIFAR-10 — 25 min  
- Construcción y entrenamiento del modelo MLP — 35 min  
- Comparación de optimizadores y ajuste de hiperparámetros — 30 min  
- Visualización de métricas en TensorBoard — 20 min  

## Desarrollo
Primero preparé el entorno importando las librerías necesarias y configurando la semilla aleatoria para mantener la reproducibilidad.  
Luego cargué el dataset **CIFAR-10** y realicé el preprocesamiento, normalizando los valores de píxel y dividiendo los datos en conjuntos de entrenamiento, validación y prueba.  

A continuación, aplané las imágenes (32×32×3 → 3072) para poder entrenar un **MLP** con dos capas densas intermedias de 32 neuronas y activación **ReLU**, más una capa de salida con activación **Softmax**.  
El modelo fue compilado con la función de pérdida `sparse_categorical_crossentropy` y el optimizador **Adam**, entrenándose durante 5 épocas con batches de 32.  

Durante el entrenamiento, visualicé las métricas de loss y accuracy en **TensorBoard**, observando cómo la red mejoraba con cada iteración.  

En esta práctica la idea fue experimentar con los **hiperparámetros** para mejorar el accuracy, por lo tanto, se manipularon los siguientes parámetros:  
- Aumentar la cantidad de **neuronas** en las capas ocultas.  
- Incrementar el número de **epochs** (por ejemplo, de 5 a 15) para permitir un aprendizaje más profundo.  
- Reducir el **learning rate** en Adam para lograr una convergencia más estable.  
- Probar con **RMSprop**, que tiende a adaptarse mejor a datasets con ruido visual como CIFAR-10.

## Evidencias
https://colab.research.google.com/drive/1dYgKfiXvHYpML0v59z4nGE1t2tbW0BiN

## Reflexión
Mediante esta práctica pude entender con mayor claridad cómo la red neuronal aprende de sus errores a través del proceso de backpropagation y cómo los distintos optimizadores influyen en la rapidez y estabilidad del entrenamiento.  
También comprobé que los hiperparámetros tienen un impacto directo en la performance del modelo, y que el equilibrio entre velocidad y precisión depende de un buen ajuste del learning rate y del número de épocas.  
Por último, confirmé que aunque los MLP funcionan bien para datos tabulares o estructurados, las imágenes requieren arquitecturas más avanzadas como las redes convolucionales (CNNs).

## Próximos pasos
Procederé a realizar la **Tarea 2 de la UT2**, donde se aplicarán redes convolucionales (CNN) para mejorar los resultados obtenidos en CIFAR-10.
