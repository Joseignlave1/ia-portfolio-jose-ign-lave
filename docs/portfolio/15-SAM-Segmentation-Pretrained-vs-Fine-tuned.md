---
title: "Entrada — Segmentación de Inundaciones con SAM: Pretrained vs Fine-Tuned"
date: 2025-11-20
---

# Entrada 15 — Segmentación de Inundaciones con SAM: Pretrained vs Fine-Tuned
~~

## Contexto
En esta actividad trabajamos con **SAM (Segment Anything Model)** para segmentar agua en escenarios de inundaciones.  
Primero evaluamos el comportamiento del modelo en su versión **pretrained**, y luego analizamos cómo cambia su desempeño tras aplicar **fine-tuning** específico para el dominio.  
El foco estuvo en entender por qué el modelo base falla, qué partes del modelo conviene ajustar y cuáles son los desafíos visuales propios de las inundaciones.

## Objetivos
- Evaluar la capacidad del SAM pretrained para segmentar agua.  
- Comprender por qué ciertos patrones visuales dañan la segmentación base.  
- Fine-tunear componentes del modelo manteniendo el encoder congelado.  
- Comparar el efecto de distintos tipos de prompts (point vs box).  
- Analizar mejoras reales obtenidas tras el fine-tuning.  
- Reflexionar sobre las limitaciones actuales del sistema y qué sería necesario para deploy real.

## Actividades (con tiempos estimados)
- Pruebas con SAM pretrained — 20 min  
- Aplicación de point prompts y box prompts — 15 min  
- Fine-tuning del decoder — 30 min  
- Comparación de resultados — 20 min  
- Reflexión general — 15 min  

## Desarrollo
Comencé evaluando el SAM pretrained sobre imágenes de inundaciones.  
El modelo generó máscaras inconsistentes: en algunos casos detectaba correctamente zonas de agua tranquila, pero fallaba en escenas con reflejos, sombras o agua mezclada con escombros.

Luego analicé el comportamiento con distintos prompts: los point prompts resultaron poco confiables, mientras que los box prompts produjeron máscaras más coherentes, especialmente en superficies amplias de agua.

Para mejorar la segmentación, realicé fine-tuning sobre el **mask decoder**, manteniendo congelado el image encoder. Esta decisión permitió adaptar el modelo al dominio sin sacrificar su capacidad de representación general.

Tras el fine-tuning, las máscaras fueron más precisas, con mejor delineación de bordes y menos confusiones con objetos flotantes o sombras pronunciadas.

## Evidencias
*https://colab.research.google.com/drive/1WjDIWOhZN6445WFF5BTBOi5iW1L6UqIZ?authuser=0#scrollTo=g5qFGtleFljP*

## Reflexión

### ¿Por qué el pretrained SAM puede fallar en detectar agua en imágenes de inundaciones efectivamente?
El pretrained SAM falla porque no fue entrenado para distinguir agua en inundaciones, un fenómeno visual complejo y altamente variable.  
El agua inundada puede parecer suelo mojado, reflejos, sombras o superficies brillantes. Sus bordes son irregulares y poco definidos, lo que confunde a un modelo generalista sin conocimiento específico del dominio.

### ¿Qué componentes de SAM decidiste fine-tunear y por qué? ¿Por qué congelamos el image encoder?
Se fine-tuneó el **mask decoder**, que es responsable de generar las máscaras finales.  
El image encoder se congela porque ya captura representaciones visuales robustas y generales. Reentrenarlo sería costoso y podría degradar su rendimiento base.  
Ajustar solo el decoder permite adaptar el modelo al dominio puntual sin perder la solidez del encoder.

### ¿Cómo se comparan point prompts vs box prompts en este caso de uso de flood segmentation?
Los point prompts ofrecieron resultados inestables: pequeños cambios en el punto alteraban mucho la máscara.  
Los box prompts fueron más confiables, ya que proporcionan al modelo un área contextual clara para delimitar.  
En inundaciones, donde los bordes son suaves y el agua se mezcla con el entorno, las cajas ayudan a obtener segmentaciones más estables.

### ¿Qué mejoras específicas observaste después del fine-tuning? (boundaries del agua, false positives, reflections, etc.)
El fine-tuning produjo mejoras visibles:  
- Bordes del agua más definidos.  
- Reducción notable de false positives, especialmente en sombras y pavimento mojado.  
- Menos confusiones con reflejos y objetos flotantes.  
- Más coherencia espacial en áreas con turbulencia o textura irregular.

### ¿Este sistema está listo para deployment en un sistema de respuesta a desastres? ¿Qué falta?
Todavía no está listo.  
Faltan:  
- Evaluación en escenarios reales más diversos.  
- Robustez ante iluminación extrema, drones a distinta altura y condiciones meteorológicas adversas.  
- Incorporación de sensores adicionales (infrarrojo o LiDAR) para validar resultados.  
- Métricas estables en tiempo real y capacidad de procesar videos completos.

### ¿Cómo cambiaría tu approach si tuvieras 10x más datos? ¿Y si tuvieras 10x menos?
Con **10x más datos**, entrenaría el decoder desde cero y consideraría descongelar parcialmente el encoder. También integraría técnicas de data balancing para cubrir más variabilidad visual.  
Con **10x menos datos**, priorizaría prompts más fuertes (box prompts), augmentations agresivos y entrenamientos tipo LoRA para evitar overfitting.

### ¿Qué desafíos específicos presenta la segmentación de agua en inundaciones? (reflections, sombras, objetos flotantes, etc.)
El agua en inundaciones presenta múltiples desafíos:  
- Reflejos que hacen que el agua parezca cielo, concreto o metal.  
- Sombras fuertes que confunden al modelo como regiones profundas o secas.  
- Objetos flotantes que rompen la continuidad del agua.  
- Bordes difusos y formas irregulares.  
- Mezcla con barro, vegetación y escombros.  
Todo esto vuelve el patrón visual altamente inconsistente y difícil de segmentar.

## Próximos pasos
Evaluar el modelo en escenarios más complejos, incorporar augmentations más realistas y preparar un pipeline que permita procesar secuencias de video en tiempo real.
