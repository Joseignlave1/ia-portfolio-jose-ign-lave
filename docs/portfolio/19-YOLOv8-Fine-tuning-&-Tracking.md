---
title: "Entrada — YOLOv8 Fine-tuning & Tracking"
date: 2025-12-07
---

# Entrada 19 — YOLOv8 Fine-tuning & Tracking

## Contexto
En este trabajo desarrollé un pipeline completo de *object detection* y *object tracking* aplicado al dominio de **productos de supermercado**. El objetivo general fue demostrar que un modelo YOLOv8 pre-entrenado en COCO no es suficiente para detectar productos específicos, y que un proceso de **fine-tuning** en un dataset especializado produce mejoras significativas en mAP, precisión, recall y calidad de los bounding boxes.  
La última etapa consistió en aplicar el modelo fine-tuned al **tracking de frutas en video**, utilizando Norfair como motor de seguimiento basado en distancias euclidianas.

Este flujo es representativo de un caso real en retail: inventario automático, conteo de productos, monitoreo de líneas de checkout y reposición en góndolas.

---

## Objetivos
- Implementar inferencia con YOLOv8 pre-entrenado en COCO.  
- Demostrar sus limitaciones en detección de productos específicos.  
- Descargar, analizar y visualizar un dataset de frutas en formato YOLO.  
- Ejecutar fine-tuning con YOLOv8n y evaluar métricas (mAP, Precision, Recall).  
- Comparar modelo base vs modelo fine-tuned antes y después del entrenamiento.  
- Analizar errores (FP, FN, IoU, bounding boxes).  
- Aplicar el modelo fine-tuned a un sistema de tracking en video con Norfair.  
- Evaluar estabilidad de IDs, calidad del tracking y métricas de duración.  

---

## Actividades (con tiempos estimados)
- Instalación y configuración del entorno — 10 min  
- Inferencia con YOLOv8 base — 10 min  
- Análisis de limitaciones del modelo base — 10 min  
- Descarga y exploración del dataset de frutas — 20 min  
- Visualización de anotaciones y distribución de clases — 20 min  
- Fine-tuning de YOLOv8 — 40 min  
- Evaluación de métricas y comparación antes/después — 20 min  
- Implementación de tracking con Norfair — 30 min  
- Análisis de calidad del tracking — 15 min  
- Reflexión final — 10 min  

---

## Desarrollo
Inicié cargando YOLOv8n pre-entrenado en COCO, realizando inferencia en imágenes de pasillos de supermercado. Esto permitió comprobar que, aunque detecta clases genéricas como *apple*, *banana* o *bottle*, no es capaz de distinguir productos específicos ni variantes de frutas empaquetadas, lo que justifica el fine-tuning.

Luego descargué el **Fruit Detection Dataset**, verifiqué su estructura YOLO (train/valid + labels), analicé la distribución de clases y visualicé ejemplos anotados. Identifiqué diferencias entre clases frecuentes y menos frecuentes, y cómo esto podría impactar las métricas posteriores.

Después ajusté el `data.yaml`, configuré hiperparámetros de entrenamiento y realicé el **fine-tuning**. Durante el entrenamiento observé el comportamiento de `box_loss`, `cls_loss` y `dfl_loss`, así como la convergencia del modelo.  

Una vez entrenado, cargué el checkpoint `best.pt`, evalué métricas en el validation set y comparé resultados frente al modelo base. El modelo fine-tuned detectó más frutas, con bounding boxes más precisos y scores de confianza más altos.

Finalmente, apliqué el modelo fine-tuned a tracking en video utilizando **Norfair**, convirtiendo cada detección en objetos `Detection` y configurando el tracker con parámetros adecuados. Analicé la estabilidad de los IDs, la continuidad de tracks y la distribución de duración de cada objeto a través del video.

---

## Evidencias
*https://colab.research.google.com/drive/1NgUKYGLodH3jsqTsA7yq_ejUVfUxl9Ob#scrollTo=ZK2y-gul8iBT*

---

## Reflexión

### Parte 1 — Modelo Base (COCO)
- El modelo base detecta solo **clases genéricas**, lo cual no es suficiente para retail.  
- Aunque COCO contenga “apple”, eso no permite distinguir variedades o productos empaquetados.  
- El número de clases (80) no incluye categorías relevantes para un supermercado real.  
- Las detecciones suelen ser poco específicas, y en muchos casos directamente ausentes.  

**Conclusión:** El fine-tuning es indispensable cuando el dominio contiene productos específicos.

---

### Parte 2 — Dataset y Fine-tuning

#### Distribución de clases
- Algunas clases están más balanceadas que otras, lo que anticipa mejor mAP en las clases con más instancias.  
- Las clases con menos ejemplos probablemente presentan más FN.  
- Si agregara más datos, priorizaría las clases menos frecuentes para mejorar recall.

#### Visualización de anotaciones
- Los bounding boxes estaban bien definidos en la mayoría de las imágenes.  
- Se observó cierta variabilidad de iluminación, fondos y tamaños, lo cual favorece la generalización.  
- Ejemplos con frutas solapadas pueden generar dificultades para el modelo.

#### Métricas de training
- `box_loss` disminuyó consistentemente, indicando mejor localización.  
- `cls_loss` se redujo, señalando mayor capacidad para distinguir clases.  
- `dfl_loss` bajó, lo que implica refinamiento en coordenadas.  
- La convergencia se alcanzó antes de los últimos epochs, justificando usar un número moderado como 10–20.

#### Hiperparámetros
- Usar fewer epochs reduce tiempo, aunque puede limitar capacidad de aprendizaje de clases raras.  
- Un tamaño de imagen mayor podría mejorar precisión, pero con mayor costo computacional.  
- FRACTION=0.25 permite entrenar rápido y aún así observar mejoras significativas, lo cual es útil en prototipos.  

---

### Parte 2 — Comparación Antes vs Después
- El modelo fine-tuned detectó **muchas más frutas** que el modelo base.  
- Las bounding boxes fueron más precisas y con mayor confianza.  
- El modelo base produjo más FP y FN, mientras que el fine-tuned redujo ambos.  
- Las clases con más instancias en el dataset tuvieron mejor mAP.  
- mAP@0.5 mejoró de forma notable, y mAP@0.5:0.95 mostró mejoras aún más pronunciadas al ser más estricto.

**Conclusión:** El fine-tuning transformó un modelo genérico en un detector especializado, altamente superior para el dominio de frutas.

---

### Parte 3 — Tracking con Norfair

#### Tracking en video
- El modelo fine-tuned permitió detectar frutas consistentemente frame a frame.  
- Los IDs se mantuvieron estables en la mayoría de objetos, aunque hubo algunos switches ocasionales.  
- Las frutas más grandes o con mayor contraste tuvieron tracking más estable.  
- Las frutas pequeñas o parcialmente ocluidas presentaron interrupciones en su track.  

#### Parámetros del tracker
- `distance_threshold` define tolerancia al movimiento; valores moderados mantuvieron la estabilidad.  
- `initialization_delay` ayudó a evitar falsos tracks creados por ruido.  
- La duración de los tracks permitió evaluar continuidad y estabilidad.  

**Conclusión:** La calidad del tracking depende tanto del modelo detector como de los parámetros del tracker.

---

## 🎯 Reflexión Final: Integración del Assignment

---

## Sobre el Modelo

### ¿Cuál fue la mejora más significativa del fine-tuning? (mAP, FPs, FNs)
La mejora más significativa fue la reducción de *false negatives* y el incremento del *mAP*, lo que demuestra que el modelo realmente aprendió las características específicas del dominio.

### ¿El modelo base (COCO) era completamente inútil o tenía algo de valor?
El modelo base no era inútil: tenía valor como punto de partida, pero era inadecuado para distinguir clases específicas del dominio. Servía como “esqueleto general” pero no como detector confiable.

### Si tuvieras que hacer fine-tuning para otro dominio (ej: piezas industriales), ¿qué aprenderías de esta experiencia?
Aprendí que, si el dominio tiene objetos bien definidos, repetir este pipeline (dataset → limpieza → fine-tuning → evaluación → tracking) permite escalar el enfoque a casi cualquier industria.

---

## Sobre los Datos

### ¿8,479 imágenes es mucho o poco para fine-tuning? ¿Por qué funcionó usar solo 25%?
8,479 imágenes es un dataset razonable para fine-tuning. Funcionar con solo 25% fue posible porque las frutas tienen formas y texturas muy distintivas y el ruido visual es bajo en la mayoría de las muestras.

### ¿La calidad de las anotaciones afectó los resultados? ¿Cómo lo sabes?
Sí, la calidad de las anotaciones influyó directamente: se observa que detecciones erróneas o bounding boxes mal posicionados generan errores consistentes en el modelo final.

### Si pudieras agregar 1,000 imágenes más, ¿de qué tipo serían?
Agregar 1,000 imágenes con:
- iluminación difícil,  
- ángulos no vistos,  
- oclusiones parciales,  
sería ideal para mejorar robustez en escenarios exigentes.

---

## Sobre el Tracking

### ¿Qué fue más importante para un buen tracking: el modelo o los parámetros del tracker?
El modelo fue más importante: un buen tracker no puede rastrear lo que no se detecta. La calidad del detector condiciona todo lo demás.

### ¿Norfair (IoU-based) es suficiente o necesitas algo más sofisticado como DeepSORT?
Norfair es suficiente para escenarios simples, pero en entornos con muchas oclusiones o múltiples objetos similares, DeepSORT u otros métodos con re-identificación serían necesarios.

### ¿Los filtros de Kalman mejoraron la estabilidad del tracking? ¿En qué situaciones?
Sí, especialmente cuando un objeto queda cubierto brevemente o se mueve rápido entre frames: el filtro predice la posición y evita saltos bruscos.

### ¿En qué escenarios fallaría este sistema de tracking?
Falla cuando:
- los objetos se superponen por mucho tiempo,  
- la cámara se mueve bruscamente,  
- hay demasiados objetos similares,  
- o el detector pierde repetidamente instancias.

---

## Sobre el Deployment

### ¿Este sistema podría correr en tiempo real? ¿Qué FPS necesitarías?
Sí, podría correr en tiempo real dependiendo del hardware. Para un supermercado o industria ligera, 20–30 FPS serían suficientes.

### ¿Qué optimizaciones harías para producción? (modelo, código, hardware)
- Exportación a TensorRT o ONNX  
- Uso de modelos más compactos  
- Cuantización  
- Pipeline asíncrono para I/O y tracking  

### ¿Cómo manejarías casos extremos? (oclusiones, iluminación, ángulos raros)
Con:
- aumentación enfocada en condiciones extremas,  
- ajustes en thresholds,  
- validación por múltiples frames,  
- modelos entrenados con iluminación difícil y ángulos atípicos.

---

## Trade-offs y Decisiones

### Identifica 3 trade-offs clave que encontraste
1. **Speed vs Accuracy**: modelos pequeños son rápidos pero menos precisos.  
2. **Epochs vs Tiempo de entrenamiento**: más entrenamiento mejora resultados pero con retornos decrecientes.  
3. **Thresholds altos vs bajos**: thresholds altos reducen *false positives* pero aumentan *false negatives*.

### ¿Cuál fue la decisión más importante que tomaste en los hyperparámetros?
Elegir un learning rate moderado y un número de epochs reducido para evitar overfitting y acelerar iteraciones experimentales fue clave.

---

## Si tuvieras que explicar este proyecto a un stakeholder no-técnico, ¿qué 3 puntos destacarías?

1. El sistema detecta productos con alta precisión y de manera automática.  
2. Puede rastrear cada objeto a lo largo del video, incluso si varios se mueven a la vez.  
3. Esto permite automatizar inventarios, monitoreo y análisis operativos sin intervención humana.

## Próximos pasos
Procedí a hacer la tarea 10 de la UT3, SAM Segmentation - Pretrained vs Fine-tuned



