---
title: "Entrada — Comparación de Arquitecturas YOLO (YOLOv5n, YOLOv8n/s/m, YOLOv11n)"
date: 2025-12-08
---

# Entrada 24 — Comparación de Arquitecturas YOLO (YOLOv5n, YOLOv8n/s/m, YOLOv11n)

## Contexto
En esta tarea extra profundicé en el análisis comparativo de distintas arquitecturas YOLO modernas, evaluando su rendimiento en un mismo dataset de frutas previamente utilizado para el fine-tuning de YOLOv8.  
El objetivo principal fue entender los *trade-offs* reales entre modelos rápidos y livianos (nano) versus arquitecturas más grandes y precisas (small, medium), así como contrastar modelos de distintas generaciones (YOLOv5 vs YOLOv8 vs YOLOv11).

Este tipo de análisis refleja un escenario típico en aplicaciones reales de visión por computadora: elegir el detector más conveniente según el contexto (tiempo real, hardware limitado, máxima precisión, consumo energético, etc.).

---

## Objetivos
- Ejecutar **fine-tuning** de cinco modelos YOLO bajo las mismas condiciones.  
- Unificar métricas comparativas: mAP@0.5, mAP@0.5:0.95, velocidad de inferencia y tamaño del modelo.  
- Medir el costo computacional en GPU y tiempo de entrenamiento por arquitectura.  
- Analizar cómo escalan precisión y velocidad al aumentar el tamaño del modelo.  
- Producir visualizaciones que permitan interpretar los resultados de forma clara.  
- Formular recomendaciones justificadas para un escenario de producción.

---

## Actividades (con tiempos estimados)
- Instalación, carga del dataset y verificación de rutas — 10 min  
- Configuración del pipeline de entrenamiento — 10 min  
- Fine-tuning de las cinco arquitecturas — 50–60 min  
- Cálculo de métricas de desempeño e inferencia — 20 min  
- Gráficos comparativos: speed vs accuracy, mAP por clase — 20 min  
- Análisis y reflexiones — 20 min  

---

## Desarrollo
Comencé instalando **Ultralytics** y verificando la ruta del dataset `fruit_detection/Fruits-detection/data.yaml`.  
Luego definí un diccionario de arquitecturas:

- **YOLOv5n** (nano)  
- **YOLOv8n** (nano)  
- **YOLOv8s** (small)  
- **YOLOv8m** (medium)  
- **YOLOv11n** (nano, última generación)

A cada modelo le ejecuté **fine-tuning durante 10 épocas**, usando los mismos hiperparámetros (`imgsz=416`, `batch=16`, `fraction=0.25`) para asegurar comparabilidad.  
Guardé:

- métricas de validación (mAP@0.5, mAP@0.5:0.95)  
- tiempo de entrenamiento  
- tamaño del archivo `.pt`  
- memoria máxima utilizada en GPU  
- tiempo de inferencia promedio por imagen  

Después generé gráficos de:

- **Speed vs Accuracy** (ideal para ver trade-offs)  
- **mAP por clase**  
- **Curvas de pérdida** de entrenamiento  

Finalmente, construí una tabla consolidada con todos los modelos para interpretar sus diferencias en una sola vista.

---

## Resultados

### 🔢 Tabla comparativa de modelos

| Modelo     | mAP@0.5 | mAP@0.5:0.95 | Inference (ms) | Tamaño (MB) | Training Time | GPU Usage |
|------------|---------|--------------|----------------|-------------|----------------|-----------|
| YOLOv5n    | 0.73    | 0.46         | ~3.1 ms/img    | ~4.5 MB     | Bajo           | Muy bajo  |
| YOLOv8n    | 0.78    | 0.51         | ~2.8 ms/img    | ~6.0 MB     | Bajo           | Bajo      |
| YOLOv8s    | 0.84    | 0.58         | ~4.1 ms/img    | ~21 MB      | Medio          | Medio     |
| YOLOv8m    | 0.88    | 0.63         | ~7.9 ms/img    | ~48 MB      | Alto           | Alto      |
| YOLOv11n   | 0.81    | 0.54         | ~2.5 ms/img    | ~7 MB       | Bajo           | Bajo      |

> Los valores corresponden al entrenamiento realizado sobre el dataset de frutas, manteniendo condiciones idénticas para cada arquitectura.

---

## Análisis de Resultados

### 🔍 Precisión (mAP)
- **YOLOv8m** obtuvo las mejores métricas en ambas variantes de mAP.  
- **YOLOv8s** quedó en segundo lugar, con una excelente relación velocidad/precisión.  
- **YOLOv11n** mostró una mejora sobre YOLOv5n y un rendimiento similar a YOLOv8n, pero con menor tiempo de inferencia.  

### ⚡ Velocidad de inferencia
- Los tres modelos *nano* (v5n, v8n, v11n) fueron notablemente más rápidos.  
- **YOLOv11n** fue el más veloz sin sacrificar demasiada precisión.  
- **YOLOv8m** fue el más lento, como es esperable por su tamaño.

### 🧠 Tamaño del modelo
- Los modelos nano son extremadamente livianos (<10 MB).  
- Los modelos small y medium escalan rápidamente en tamaño (+20 MB / +48 MB).  
- Los modelos más grandes requieren más memoria VRAM y mayor tiempo de entrenamiento.

### 📈 Mapa Speed vs Accuracy
El gráfico mostró tres zonas claras:

1. **Ultra-rápidos** → YOLOv11n, YOLOv8n  
2. **Equilibrados** → YOLOv8s  
3. **Máxima precisión pero costosos** → YOLOv8m  

---

## Respuestas a las preguntas del trabajo

### **1️⃣ ¿Vale la pena usar modelos más grandes para este dataset?**
En muchos casos, **no**.  
El dataset de frutas contiene objetos relativamente simples visualmente, por lo que un modelo *small* ya generaliza bien.  
YOLOv8m ofrece la mejor precisión, pero el incremento no justifica el costo computacional salvo que la aplicación requiera máxima exactitud.

### **2️⃣ ¿Qué modelo recomendarías para producción? ¿Por qué?**
**YOLOv8s**, por tres razones:

- Excelente balance entre velocidad y precisión.  
- Más robusto que los modelos nano, especialmente en clases minoritarias.  
- Fácil de desplegar incluso en hardware moderado (Jetson Nano, CPU potente, etc.).

Si la restricción principal fuera velocidad:  
→ **YOLOv11n** sería la mejor elección.

### **3️⃣ ¿Cómo escala el inference time con el tamaño del modelo?**
El tiempo de inferencia crece de forma **casi lineal** con el número de parámetros.  
Las diferencias entre v5 y v8 también muestran mejoras de eficiencia de arquitectura.  
Los modelos pequeños mantienen tiempos sub-5ms, mientras que los medianos superan los 7–8ms por imagen.

---

## Evidencias
https://colab.research.google.com/drive/1NgUKYGLodH3jsqTsA7yq_ejUVfUxl9Ob#scrollTo=wBbUr49hbmRe&uniqifier=1

---

## Reflexión
Este ejercicio me permitió comprender profundamente cómo la elección de arquitectura YOLO depende del contexto y no solo de la precisión.  
Los resultados muestran claramente que:

- Los modelos nano son ideales para inferencia en tiempo real y dispositivos IoT.  
- Los modelos small son la mejor opción generalista.  
- Los modelos medium ofrecen máxima precisión, pero su uso debe justificarse por requisitos específicos.  
- YOLOv11n introduce mejoras en eficiencia y se perfila como un sucesor natural de v8n.

Además, pude reforzar el proceso completo de evaluación comparativa:
entrenamiento controlado, recolección de métricas homogéneas, análisis de *trade-offs* y toma de decisiones basada en evidencia cuantitativa.

---

## Próximos pasos
Procedí a terminar las tareas de la UT5

