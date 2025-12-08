---
title: "Entrada 11 — Backpropagation y Optimizadores con Fashion-MNIST"
date: 2025-10-15
---

# Entrada 12 — Backpropagation y Optimizadores con Fashion-MNIST~~
~~

## Contexto
Como ejercicio adicional a la práctica de backpropagation y optimizadores, repetí el pipeline completo de entrenamiento visto en clase, pero aplicándolo a un nuevo dataset: **Fashion-MNIST**.  
Este dataset contiene 70.000 imágenes en escala de grises de 28×28 distribuidas en 10 clases de prendas, lo que lo convierte en un punto intermedio ideal entre MNIST y CIFAR-10: más complejo que dígitos, pero menos ruidoso que imágenes en color.  

El objetivo fue reforzar los conceptos trabajados en la práctica original, verificando cómo reacciona la misma arquitectura MLP ante un dominio diferente, y evaluar si los ajustes de hiperparámetros se comportan de manera similar o requieren calibración.

## Objetivos
- Replicar el pipeline de la práctica original utilizando un dataset diferente.  
- Preprocesar imágenes (normalización, reshape) para adaptarlas al modelo.  
- Entrenar un MLP sobre Fashion-MNIST utilizando TensorFlow/Keras.  
- Analizar la performance mediante accuracy, loss, matriz de confusión y classification report.  
- Comparar la estabilidad del entrenamiento con Adam frente a otros optimizadores.  

## Actividades (con tiempos estimados)
- Carga y normalización del dataset — 15 min  
- Aplanamiento de imágenes y preparación del set de entrenamiento/validación — 10 min  
- Construcción del modelo MLP — 20 min  
- Entrenamiento con distintos optimizadores — 40 min  
- Evaluación final y análisis de métricas — 20 min  

## Desarrollo
Comencé cargando **Fashion-MNIST** directamente desde Keras y normalizando los valores de píxel a \[-1, 1\], tal como hicimos en el trabajo con CIFAR-10.  
Luego dividí el conjunto en entrenamiento, validación y prueba, y aplané las imágenes (28×28 → 784) para poder entrenar una red totalmente conectada.

La arquitectura que utilicé consistió en:
- Una capa densa inicial de 128 neuronas con activación **ReLU**.  
- Una segunda capa densa de 64 neuronas también con **ReLU**.  
- Una capa de salida de 10 neuronas con **softmax**.  

El entrenamiento se realizó con **Adam**, función de pérdida `sparse_categorical_crossentropy` y métricas de accuracy, durante 10 épocas.  
Después, repetí el entrenamiento probando **SGD con momentum** y **RMSprop**, comparando cómo cambiaba la convergencia y la estabilidad del loss.  

En este dataset el MLP mostró mejor capacidad de generalización que en CIFAR-10, alcanzando valores de accuracy más altos (~87–89%) aun sin regularización adicional.

Finalmente, generé la matriz de confusión y el classification report para observar qué clases presentaban mayor confusión (principalmente *shirt*, *t-shirt/top* y *pullover*).

## Evidencias
https://colab.research.google.com/drive/178b4uB7XWH1C3v_7z2GxkqI-kjCt1mgv?authuser=0#scrollTo=rf23F-YPOho3&uniqifier=2

## Reflexión
Esta práctica me permitió confirmar cómo la **complejidad del dataset** afecta directamente la capacidad de un MLP para aprender patrones visuales.  
Fashion-MNIST, al ser más simple que CIFAR-10, ofreció un escenario más favorable para evaluar la influencia del optimizador, el learning rate y la arquitectura sin que el ruido visual domine el proceso.

Pude verificar también que:
- Adam sigue siendo el optimizador más estable para este tipo de tareas.  
- El número de épocas tiene un impacto más marcado que en CIFAR-10, ya que el modelo converge más rápido pero sigue mejorando con entrenamiento adicional.  
- Los errores de clasificación se concentran en prendas similares, lo que demuestra las limitaciones del MLP para capturar matices visuales sin convoluciones.

## Próximos pasos
Me gustaría repetir el experimento utilizando **convoluciones (CNN)** para comparar directamente contra el MLP, y así medir cuánto mejora la capacidad de representación al usar una arquitectura más adecuada para imágenes.
