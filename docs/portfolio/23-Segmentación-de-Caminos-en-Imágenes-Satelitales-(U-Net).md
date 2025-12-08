---
title: "Entrada — Segmentación de Caminos en Imágenes Satelitales (U-Net)"
date: 2025-12-07
---

# Entrada 23 — Segmentación de Caminos en Imágenes Satelitales con U-Net  
~~

## Contexto
En esta actividad extra trabajé con el dataset **DeepGlobe Road Extraction**, un conjunto de imágenes satelitales pensado para el desafío de segmentar caminos desde vista aérea.  
A diferencia de la segmentación de inundaciones con SAM, este ejercicio se enfocó en un modelo **U-Net entrenado desde cero**, lo cual permite estudiar en profundidad cómo aprende una red totalmente supervisada para mapas de carreteras.

El objetivo fue construir un pipeline completo: preparar el dataset, crear una arquitectura U-Net compacta, entrenarla con estrategias estándar de segmentación y evaluar la calidad de las predicciones utilizando métricas como **IoU** y **Dice**.

Este tipo de sistema es relevante en cartografía automática, planificación urbana, actualización de GIS y análisis de infraestructura vial.

---

## Objetivos
- Preparar y limpiar un dataset real de segmentación aérea.  
- Implementar un pipeline eficiente con `tf.data`.  
- Construir un modelo **U-Net** desde cero.  
- Entrenar la red y monitorear métricas globales (loss, IoU, Dice).  
- Visualizar predicciones y comparar contra máscaras reales.  
- Reflexionar sobre limitaciones, desafíos visuales y oportunidades de mejora.

---

## Actividades (con tiempos estimados)
- Descarga y organización del dataset — 20 min  
- Exploración de la estructura y validación de máscaras — 15 min  
- Implementación del loader y preprocesamiento — 20 min  
- Construcción del modelo U-Net — 20 min  
- Entrenamiento y análisis de curvas de aprendizaje — 30 min  
- Evaluación cualitativa y cuantitativa — 15 min  
- Conclusión y reflexiones — 10 min  

---

## Desarrollo
Comencé descargando el dataset desde Kaggle y verificando su estructura.  
Aunque inicialmente las carpetas estaban organizadas en *train/test/valid*, fue necesario reconstruir un **split manual** entre imágenes satelitales “\*_sat.jpg” y sus máscaras correspondientes “\*_mask.png”.  
Finalmente obtuve un split consistente con:

- **4980 imágenes** para entrenamiento  
- **1246 imágenes** para validación  
- Todas con máscaras correctamente emparejadas  

A continuación implementé funciones de preprocesamiento en TensorFlow:  
- Redimensionado a 256×256  
- Normalización de imágenes  
- Binarización de máscaras  
- Pipeline eficiente con `tf.data` y `prefetch`

Luego construí una **U-Net compacta**, con bloques encoder–decoder simétricos y skip connections que permiten preservar detalles espaciales finos, fundamentales para caminos delgados.

El modelo se entrenó con `Adam (1e-4)` y pérdida `binary_crossentropy`, añadiendo métricas personalizadas de **IoU** y **Dice**, más adecuadas para segmentación binaria.

Durante el entrenamiento, las curvas mostraron mejoras constantes:  
- El IoU aumentó gradualmente, indicando una buena recuperación de formas y continuidad de caminos.  
- La pérdida de validación se mantuvo estable, lo que sugiere ausencia de overfitting significativo a 20 épocas.  

Tras el entrenamiento, probé el modelo en el conjunto de validación.  
Las predicciones lograron recuperar caminos principales con buena continuidad, especialmente en zonas rurales o de baja densidad.  
Las regiones urbanas y caminos angostos presentaron mayores dificultades, lo cual es esperable dadas las variaciones de textura, sombras y oclusiones propias del dataset.

---

## Evidencias
https://colab.research.google.com/drive/1Nfh5Rc9bXcC6SclI-VZ9IkZtpEcT9hh6?usp=sharing

---

## Reflexión

### ¿Por qué U-Net es una buena arquitectura para segmentación de caminos?
U-Net combina **captura global de contexto** (encoder) con **recuperación local de detalles** (decoder).  
Los caminos suelen ser estructuras delgadas y continuas, por lo que los *skip connections* son esenciales para no perder información espacial fina durante el downsampling.

### ¿Cuáles fueron los desafíos más visibles del dataset?
- Sombras de árboles y edificaciones que rompen la continuidad del camino.  
- Áreas donde los caminos están deteriorados o cubiertos parcialmente.  
- Variaciones fuertes de color entre regiones urbanas y rurales.  
- Calles muy estrechas que pueden confundirse con bordes de edificios.

### ¿Qué tan bien funcionó la U-Net compacta?
El modelo logró buenas segmentaciones generales, especialmente en caminos principales.  
El IoU alcanzó valores sólidos para un entrenamiento rápido y sin augmentations.  
Sin embargo, caminos angostos o visualmente confusos fueron más difíciles de resolver.

### ¿Qué mejorarías si entrenaras nuevamente?
- Añadir **data augmentation** realista (sombras, brillo, blur).  
- Aumentar la resolución del input (512×512).  
- Probar una U-Net++ o DeepLabv3+ para captar contextos más amplios.  
- Ajustar la pérdida para favorecer clases minoritarias (roads < background).

### ¿Este modelo está listo para producción?
No todavía.  
Necesitaría:  
- Entrenamiento más prolongado.  
- Evaluación en nuevos dominios geográficos.  
- Validación externa con especialistas GIS.  
- Manejo de imágenes de mayor resolución y variedad.

---

## Conclusión Final
Este trabajo permitió comprender cómo una arquitectura completamente supervisada aprende a segmentar carreteras desde cero.  
La U-Net demostró ser efectiva y eficiente, y el pipeline resultante es una base sólida para tareas más avanzadas como segmentación multiclase o mapeo automático a gran escala.

## Próximos pasos
Aplicar este mismo pipeline a un dataset multiclase de segmentación aérea, como **Aeroscapes** o **DeepGlobe Land Cover**, para introducir clasificación semántica más compleja.
