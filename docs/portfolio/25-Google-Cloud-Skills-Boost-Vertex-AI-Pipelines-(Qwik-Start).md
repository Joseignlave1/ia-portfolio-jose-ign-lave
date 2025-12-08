---
title: "Entrada — Google Cloud Skills Boost: Vertex AI Pipelines (Qwik Start)"
date: 2025-11-20
---

# Entrada 25 — Google Cloud Skills Boost: Vertex AI Pipelines (Qwik Start)  
~~

## Contexto
Este lab forma parte del módulo introductorio de Google Cloud Skills Boost orientado a comprender el funcionamiento básico de **Vertex AI Pipelines**.  
El propósito fue practicar la apertura de un entorno de Workbench, instalar dependencias, compilar componentes simples en Kubeflow Pipelines y ejecutar canalizaciones tanto básicas como de aprendizaje automático de extremo a extremo.

El foco estuvo en seguir paso a paso el flujo estándar de Vertex AI Pipelines: creación del notebook, definición de componentes, compilación, ejecución y verificación en la consola.

## Objetivos
- Acceder a Vertex AI Workbench usando credenciales temporales.  
- Instalar el SDK de Kubeflow Pipelines y las librerías complementarias.  
- Crear y ejecutar una canalización introductoria de tres pasos.  
- Definir un componente personalizado para evaluar métricas de AutoML.  
- Crear una canalización completa que entrena, evalúa y despliega un modelo Tabular AutoML.

## Actividades (con tiempos estimados)
- Apertura del notebook en Vertex AI Workbench — 5 min  
- Instalación de dependencias y reinicio de kernel — 10 min  
- Creación de componentes simples (`product_name`, `emoji`, `build_sentence`) — 15 min  
- Compilación y ejecución de la canalización introductoria — 10 min  
- Definición del componente de evaluación y de la canalización AutoML — 35 min  
- Compilación y ejecución del job de AutoML — 15 min  

## Desarrollo
Al iniciar el lab accedí a Vertex AI Workbench desde la consola con el usuario temporal proporcionado. Allí abrí un notebook nuevo, lo renombré y ejecuté las instrucciones para instalar `kfp`, `google-cloud-aiplatform`, `google_cloud_pipeline_components` y las dependencias adicionales necesarias para evitar conflictos con `shapely` y `geopandas`. Tras eso reinicié el kernel y verifiqué las versiones instaladas.

Luego configuré las variables del proyecto (`PROJECT_ID`, `BUCKET_NAME`, `REGION`) y definí el `PIPELINE_ROOT`. Importé todas las librerías requeridas para ejecutar canalizaciones.

La primera parte del lab consistió en crear una canalización simple:  
- un componente que devuelve un texto,  
- un componente que convierte una cadena en emoji,  
- y un componente final que construye una frase combinando ambos resultados.  

Tras definirlos, compilé la canalización (`intro_pipeline`) y la ejecuté mediante `AIPlatformClient`. En Vertex AI Pipelines pude visualizar el DAG con los tres pasos y verificar que se ejecutaran correctamente.

En la segunda parte definí un componente personalizado para evaluar métricas de un modelo AutoML, incluyendo la lectura del AUC y el registro de matriz de confusión y curva ROC. Con esto construí una canalización más completa:  
1) creación del dataset tabular en Vertex AI,  
2) entrenamiento AutoML,  
3) evaluación mediante el componente personalizado,  
4) decisión condicional de despliegue,  
5) despliegue opcional en un endpoint.  

Compilé esta canalización y ejecuté el job usando `create_run_from_job_spec`. El objetivo del lab era confirmar que el entrenamiento comenzara correctamente, algo que verifiqué desde la consola.

## Reflexión
Este lab me permitió seguir el flujo completo para crear canalizaciones en Vertex AI: desde la configuración del notebook, la instalación de dependencias, la definición de componentes y la compilación, hasta la ejecución en la consola y la verificación de artefactos.  
También pude ver cómo se integran los servicios de Vertex AI dentro de una canalización, especialmente en tareas de AutoML Tabular.

La experiencia reforzó el uso práctico del SDK de Kubeflow Pipelines en GCP y la estructura necesaria para automatizar flujos de trabajo de machine learning de manera reproducible.