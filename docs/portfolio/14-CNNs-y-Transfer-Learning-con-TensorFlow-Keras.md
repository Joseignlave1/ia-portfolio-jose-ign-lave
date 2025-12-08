---
title: "Entrada 13 — UT3 CNNs y Transfer Learning con TensorFlow/Keras"
date: 2025-10-25
---

# Entrada 14— CNNs y Transfer Learning con TensorFlow-Keras~~
~~

## Contexto
En este trabajo práctico exploramos la creación de modelos de visión por computadora utilizando TensorFlow/Keras.  
El objetivo fue comparar el desempeño entre una **CNN construida desde cero** y un modelo basado en  
**Transfer Learning**, utilizando arquitecturas pre-entrenadas de *Keras Applications*.  

También trabajamos con el dataset **CIFAR-10**, realizando la preparación de los datos, normalización de imágenes,  
configuración del batch size y posterior entrenamiento de ambos modelos para analizar su comportamiento  
en términos de precisión, generalización y riesgo de overfitting.

## Objetivos
- Comprender la arquitectura básica de una CNN implementada desde cero.  
- Implementar *transfer learning* utilizando un modelo pre-entrenado.  
- Entrenar y evaluar ambos modelos utilizando TensorFlow/Keras.  
- Analizar curvas de pérdida y precisión para interpretar el aprendizaje.  
- Comparar el rendimiento entre CNN simple y Transfer Learning.  
- Detectar y evaluar señales de overfitting en cada modelo.  

## Actividades (con tiempos estimados)
- Revisión del dataset CIFAR-10 y normalización — 15 min  
- Implementación de la CNN y configuración de sus capas — 30 min  
- Implementación del modelo con Transfer Learning — 30 min  
- Entrenamiento y análisis de ambos modelos — 40 min  
- Revisión de métricas, gráficas e interpretación final — 20 min  

## Desarrollo
Comencé cargando el dataset CIFAR-10, analizando su composición y normalizando las imágenes para  
prepararlas correctamente para el entrenamiento. Luego construí una **CNN simple**, utilizando capas convolucionales,  
max pooling, y una capa totalmente conectada final para la clasificación de las diez categorías del dataset.

Posteriormente implementé un modelo utilizando **Transfer Learning**, seleccionando una arquitectura de  
*Keras Applications* y cargando sus pesos pre-entrenados en ImageNet. Las capas del modelo base se mantuvieron  
congeladas inicialmente, agregando únicamente una capa final *Dense* como clasificador.

Una vez configurados ambos modelos, los entrené utilizando *EarlyStopping* para controlar el sobreajuste  
y comparé sus métricas de rendimiento. El modelo basado en Transfer Learning obtuvo mayor precisión  
y mostró un comportamiento más estable, mientras que la CNN simple tendió a sobreajustarse a las primeras épocas.

Por último, analicé las curvas de entrenamiento y validación, el nivel de overfitting observado en cada caso,  
y los reportes de clasificación para evaluar de manera más detallada el desempeño de cada arquitectura.

## Evidencias
https://colab.research.google.com/drive/15MpvVBOZ9MGbD9lER5thpccZJDmTjF3d#scrollTo=buqnq2gWDj5K

## Reflexión
Este trabajo me permitió comprender mejor cómo se construyen y entrenan modelos de visión por computadora en TensorFlow/Keras,  
y por qué los modelos pre-entrenados suelen ofrecer mejores resultados en datasets pequeños o con alta variabilidad.  

Además, pude observar cómo parámetros como el learning rate, el número de capas entrenables y el tamaño de los batches  
influyen directamente en el rendimiento. Las curvas de entrenamiento, junto con las métricas finales, fueron útiles  
para diagnosticar el comportamiento de cada modelo y entender sus ventajas y limitaciones.

En general, este trabajo reforzó mi comprensión de CNNs y Transfer Learning, y sentó las bases para seguir  
profundizando en arquitecturas más avanzadas en visión por computadora.

## Próximos pasos
Procedí a realizar la Tarea Data Augmentation Avanzado & Explicabilidad - Fill in the Blanks de la UT3
