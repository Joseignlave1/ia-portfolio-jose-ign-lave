---
title: "Entrada 06 — Clustering y PCA: Segmentación de Clientes"
date: 2025-09-21
---

# Entrada 06 — Sexto trabajo práctico

## Contexto
En este trabajo práctico exploramos técnicas de **segmentación de clientes** aplicando algoritmos de clustering y reducción de dimensionalidad.  
Se utilizó el dataset **Mall Customer Segmentation**, que contiene información demográfica y de comportamiento de ~200 clientes.  
El objetivo fue descubrir patrones en el gasto y los ingresos, con el fin de crear perfiles útiles para estrategias de marketing.  

El flujo de trabajo se guió con la metodología **CRISP-DM**, pasando por fases de comprensión del negocio, preparación de datos, modelado y evaluación.  

## Objetivos
- Entender la importancia de la fase de *Business Understanding* en problemas de segmentación.  
- Aplicar normalización con diferentes scalers (MinMax, Standard, Robust) y evaluar su impacto en clustering.  
- Usar **PCA** para reducir la dimensionalidad y visualizar los datos en 2D.  
- Comparar **PCA** con técnicas de selección de features (Forward, Backward, RFE).  
- Identificar el número óptimo de clusters usando **Elbow Method** y **Silhouette Score**.  
- Aplicar diferentes algoritmos de clustering (KMeans, DBSCAN, HDBSCAN, GMM, Spectral, Agglomerative).  
- Evaluar interpretabilidad vs performance en un contexto real de negocio.  

## Actividades (con tiempos estimados)
- Exploración inicial del dataset y estadísticas descriptivas — 20 min  
- Análisis de escalas y aplicación de scalers — 30 min  
- Implementación de PCA y visualización en 2D — 40 min  
- Ejecución de KMeans con búsqueda de K óptimo (Elbow + Silhouette) — 45 min  
- Pruebas con otros algoritmos (DBSCAN, HDBSCAN, GMM, Spectral, Agglomerative) — 60 min  
- Ejercicios de selección de features (Forward, Backward, RFE) y comparación con PCA — 50 min  
- Redacción de reflexiones finales y preguntas guía — 30 min  

## Desarrollo
Comencé cargando el dataset de clientes del centro comercial y realicé un análisis exploratorio de sus principales variables:  
edad, ingresos anuales y spending score.  
También verifiqué la distribución por género y detecté la presencia de algunos outliers.  

En la fase de preparación de datos, probé tres escalers (MinMax, Standard y Robust) y evalué cuál impactaba mejor en el clustering.  
Luego apliqué **PCA** para reducir a 2 dimensiones y visualizar la varianza explicada, confirmando que con dos componentes se podía capturar más del 90% de la información relevante.  

En la parte de clustering, usé **KMeans** con un rango de K entre 2 y 8.  
El **Elbow Method** y el **Silhouette Score** no coincidieron exactamente, pero ajustando al contexto de negocio (3–5 clusters esperados), elegí un valor de K coherente con ambas métricas.  
Los clusters resultantes mostraron diferencias claras entre niveles de ingreso y gasto, lo que coincide con perfiles típicos de clientes en marketing.  

Más adelante, probé otros algoritmos:  
- **DBSCAN/HDBSCAN** para clusters de densidad irregular.  
- **Gaussian Mixture Models** para clustering probabilístico.  
- **Spectral y Agglomerative Clustering** para comparar enfoques jerárquicos y espectrales.  

Finalmente, complementé el análisis con **Feature Selection (Forward, Backward, RFE)** y lo comparé con PCA.  
PCA resultó más efectivo en performance y visualización, aunque Feature Selection mantiene más interpretabilidad.  

## Reflexiones finales

### Metodología CRISP-DM
- La fase más desafiante fue *Data Preparation*, porque tuve que probar distintos scalers y métodos de reducción dimensional, con varias iteraciones para mejorar el clustering.  
- El entendimiento del negocio fue clave al decidir el número de clusters: aunque las métricas sugerían valores distintos, en un contexto real tiene más sentido trabajar con 3–5 segmentos.  

### Data Preparation
- El scaler más efectivo fue **PCA con datos previamente normalizados**, porque capturó la mayor parte de la varianza y mejoró el silhouette score.  
- PCA fue más útil que Feature Selection, ya que permitió visualizar clusters y mejorar el rendimiento.  
- El balance entre interpretabilidad y performance se inclinó hacia la performance, pero siempre considerando que en un negocio habría que traducir los componentes en insights concretos.  

### Clustering
- Elbow Method y Silhouette no coincidieron del todo, pero con el contexto de negocio se eligió un K apropiado.  
- Los clusters encontrados tienen sentido desde la intuición: clientes con alto ingreso/bajo gasto, bajo ingreso/alto gasto, y perfiles intermedios.  
- Si repitiera el análisis, probaría más algoritmos (como DBSCAN o Agglomerative) para validar la robustez de los resultados.  

### Aplicación práctica
- En un entorno empresarial, presentaría los resultados con visualizaciones claras (mapas de calor, PCA, t-SNE, UMAP) para mostrar cómo se diferencian los grupos.  
- El valor de la segmentación es claro: diseñar campañas personalizadas, optimizar recursos y mejorar la efectividad de la inversión publicitaria.  
- La principal limitación es la simplicidad del dataset y el supuesto de clusters esféricos de KMeans, que puede no reflejar la realidad.  

## Preguntas guía

- **¿Qué algoritmo funciona mejor con clusters de densidad variable?**  
  DBSCAN o HDBSCAN.  

- **¿Cuándo usar clustering jerárquico vs particional?**  
  Jerárquico cuando se buscan dendrogramas o estructura jerárquica, particional (KMeans, GMM) cuando ya se conoce el número de clusters.  

- **¿Cómo afecta la dimensionalidad a diferentes algoritmos?**  
  Algoritmos como KMeans sufren en alta dimensión; conviene aplicar reducción como PCA, t-SNE o UMAP primero.  

- **¿Qué ventajas tiene RFE sobre Forward/Backward selection?**  
  RFE es iterativo y considera interacciones entre features, mientras que Forward/Backward son más simples pero pueden pasar por alto combinaciones óptimas.  

## Evidencias
https://colab.research.google.com/drive/xxxx?usp=sharing  

## Reflexión  
Mediante este trabajo, pude aprender en profundidad el uso de distintos algoritmos de clustering  
y cómo la reducción de dimensionalidad con PCA ayuda a visualizar y mejorar la calidad de los segmentos.  

También comprendí la importancia de la fase de preparación de datos,  
ya que la elección del scaler y de la técnica de reducción influye directamente en la separación de los clusters.  

Por último, afianzé el concepto de cómo elegir el número óptimo de clusters con métodos como Elbow y Silhouette,  
y entendí que, más allá de las métricas, siempre es necesario considerar el contexto de negocio para que la segmentación sea realmente útil.  

Este trabajo me permitió valorar la diferencia entre interpretabilidad y performance,  
y ver cómo cada técnica (PCA, Feature Selection, DBSCAN, GMM, etc.) aporta distintas perspectivas para el análisis.  

## Próximos pasos
En próximas prácticas quiero comparar formalmente los algoritmos de clustering alternativos (DBSCAN, HDBSCAN, GMM)  
y explorar cómo combinarlos con técnicas de visualización como t-SNE y UMAP para datasets de mayor dimensionalidad.  
