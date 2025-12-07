---
title: "Entrada 13 — Robustez y Explicabilidad en Computer Vision con TensorFlow/Keras"
date: 2025-11-02
---

# Entrada 13 — Data Augmentation Avanzado & Explicabilidad Fill in the Blanks
~~

## Contexto
En este trabajo práctico exploramos técnicas avanzadas de visión por computadora orientadas a mejorar la **robustez**,  
la **generalización** y la **explicabilidad** de modelos basados en *transfer learning* aplicados a imágenes de alta resolución.

El dataset utilizado fue **Oxford Flowers102**, un dataset complejo y desbalanceado con 102 especies de flores.  
El objetivo fue construir un pipeline profesional de entrenamiento que combine augmentation avanzado,  
técnicas modernas como Mixup/CutMix, y herramientas de interpretabilidad como GradCAM e Integrated Gradients.

## Objetivos
- Preparar datasets de imágenes de alta resolución utilizando TensorFlow Datasets.  
- Implementar pipelines de *data augmentation* profesionales con Keras Preprocessing Layers.  
- Explorar técnicas avanzadas como **Mixup** y **CutMix**.  
- Entrenar modelos robustos basados en *transfer learning* (EfficientNetB0/MobileNetV2).  
- Aplicar **GradCAM** para visualizar la atención del modelo.  
- Aplicar **Integrated Gradients** para interpretar contribuciones por píxel.  
- Comparar el desempeño entre un baseline y un modelo con augmentation avanzado.  
- Reflexionar sobre la importancia de la explicabilidad en aplicaciones reales.  

## Actividades (con tiempos estimados)
- Descarga y preparación del dataset Flowers102 — 20 min  
- Construcción del pipeline baseline y pipeline con augmentation avanzado — 40 min  
- Visualización de augmentations generados — 15 min  
- Implementación del modelo con transfer learning (EfficientNetB0) — 20 min  
- Entrenamiento del modelo — 40 min  
- Aplicación de GradCAM e Integrated Gradients — 40 min  
- Respuesta a preguntas teóricas y análisis de robustez — 30 min  

## Desarrollo
Inicié cargando el dataset **Oxford Flowers102** desde TensorFlow Datasets y creando una función de preprocesamiento  
que normaliza las imágenes y uniformiza su tamaño a 224×224 píxeles. Para acelerar los experimentos utilicé subsets del dataset,  
respetando sus proporciones originales.

Luego construí dos pipelines de datos:  
1. **Pipeline baseline**, sin augmentations avanzados, que aplica únicamente normalización.  
2. **Pipeline con augmentation avanzado**, donde incorporé transformaciones geométricas  
(*RandomFlip, RandomRotation, RandomZoom, RandomTranslation*) y fotométricas  
(*RandomBrightness, RandomContrast*).  

Esto permitió obtener un dataset de entrenamiento más variado y robusto, especialmente útil dado el desbalance de clases.

Posteriormente, implementé el modelo principal utilizando **EfficientNetB0** con *transfer learning*, congelando inicialmente  
las capas del modelo base y agregando una capa final *Dense* de 102 neuronas para clasificar las especies del dataset.  
Este enfoque redujo el tiempo de entrenamiento y aumentó la capacidad de generalización.

Una vez entrenado el modelo, analicé la precisión alcanzada y generé gráficos de accuracy y loss para evaluar su desempeño.  
Luego apliqué **GradCAM**, que permitió visualizar qué regiones de la imagen influían más en cada predicción,  
y **Integrated Gradients**, para obtener un mapa más detallado de la contribución de cada píxel.

Finalmente, respondí las preguntas de reflexión, analizando errores del modelo,  
su comportamiento ante perturbaciones y la importancia de explicabilidad en aplicaciones reales.

## Evidencias
https://colab.research.google.com/drive/18flXNNdGkKyj7naNaawL3b7RzUjtvt-y#scrollTo=VBtCTrq5JNT1&uniqifier=1

## Reflexión
Este trabajo me permitió profundizar en técnicas modernas de visión computacional que van más allá del entrenamiento estándar.  
El uso de augmentation avanzado mejoró notablemente la robustez del modelo, reduciendo su dependencia a condiciones de iluminación o ángulos específicos.

También pude observar la importancia de la explicabilidad en modelos de visión:  
herramientas como GradCAM e Integrated Gradients permiten validar que el modelo “mire” las regiones correctas,  
lo cual es crucial en un contexto real como el de la identificación botánica.

A continuación respondo las preguntas de reflexión solicitadas:

### 1. Data Augmentation  
El data augmentation tuvo un impacto positivo en el modelo: la accuracy de validación mejoró respecto al pipeline baseline.  
Esto ocurre porque las transformaciones geométricas y fotométricas generan variaciones de la misma imagen,  
permitiendo que el modelo aprenda representaciones más robustas y generales, reduciendo el riesgo de overfitting  
y mejorando su capacidad para manejar condiciones reales como cambios de luz, ángulo y fondo.

### 2. GradCAM  
Al analizar varias predicciones con GradCAM, pude verificar que el modelo generalmente se enfocaba en regiones relevantes de la flor,  
como pétalos, patrón de color o centro de la misma. En algunos casos me sorprendió que ignorara partes visualmente importantes  
para un humano, pero aun así lograba predecir correctamente. Esto demuestra que el modelo aprende representaciones distintas  
a las que usaría una persona, pero igualmente efectivas.

### 3. Errores del Modelo  
En uno de los ejemplos donde el modelo se equivocó, GradCAM mostró que la atención estaba dispersa en el fondo  
y no en la flor principal. Esto sugiere que la imagen tenía elementos distractores o una flor poco distinguible,  
por lo que el modelo no logró identificar patrones consistentes. La visualización permitió entender  
que el error no fue aleatorio, sino consecuencia de una atención mal dirigida.

### 4. Aplicación Práctica  
En una aplicación de identificación de flores, la explicabilidad es fundamental para generar confianza en los usuarios.  
Poder mostrar *por qué* el modelo predice una especie en particular ayuda a validar su comportamiento  
y evita que se perciba como una “caja negra”.  
Sin explicabilidad, un error podría llevar a confusiones botánicas, instrucciones de cuidado incorrectas  
o pérdida de credibilidad de la aplicación.

### 5. Mejoras del Modelo  
Si tuviera más tiempo para continuar este trabajo, exploraría:
- **Más datos** o técnicas de oversampling para equilibrar clases.  
- **Fine-tuning** de capas superiores de EfficientNetB0.  
- **Más épocas** de entrenamiento con early stopping.  
- **Modelos más grandes** como EfficientNetB2/B3.  
- Evaluación con **Mixup/CutMix** para verificar mejoras de robustez adicionales.  

## Próximos pasos
Procedí a realizar la tarea YOLOv8 Fine-tuning & Tracking de la UT3
