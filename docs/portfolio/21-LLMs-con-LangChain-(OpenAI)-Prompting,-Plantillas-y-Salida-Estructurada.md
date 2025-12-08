---
title: "Entrada 15 — LLMs con LangChain (OpenAI): Prompting, Plantillas y Salida Estructurada"
date: 2025-11-14
---

# Entrada 21 — LLMs con LangChain (OpenAI): Prompting, Plantillas y Salida Estructurada
~~

## Contexto
En este trabajo práctico exploramos el flujo completo para construir aplicaciones modernas utilizando **LLMs de OpenAI integrados con LangChain**,  
enfocados en prompting profesional, control de decodificación, plantillas reutilizables, salidas estructuradas  
y trazabilidad mediante LangSmith.

El objetivo fue adquirir las bases para construir pipelines robustos de LLMs: desde cómo instanciar un modelo en LangChain,  
hasta cómo garantizar salidas JSON válidas mediante Pydantic, pasando por técnicas modernas de prompting, zero-shot/few-shot  
y un primer acercamiento a RAG.

## Objetivos
- Instanciar modelos de OpenAI mediante `ChatOpenAI` y ejecutar invocaciones básicas.  
- Controlar parámetros de decodificación (*temperature*, *max_tokens*, *top_p*)
  y analizar su impacto en creatividad, claridad y determinismo.  
- Crear prompts reutilizables con **ChatPromptTemplate** y encadenarlos con LCEL (`|`).  
- Obtener salidas estructuradas validadas mediante **with_structured_output(...)** sin necesidad de parseo manual.  
- Medir tokens y latencia con LangSmith como base de observabilidad.  
- Implementar mini-tareas prácticas: traducción determinista, resúmenes ejecutivos, Q&A con contexto limitado,  
  zero-shot vs few-shot, extracción de entidades y RAG básico.  

## Actividades (con tiempos estimados)
- Instalación y setup inicial — 15 min  
- Instanciación del modelo y primeras pruebas — 15 min  
- Experimentos con temperatura, top_p y max_tokens — 20 min  
- Construcción de plantillas con ChatPromptTemplate — 20 min  
- Salida estructurada con Pydantic — 20 min  
- Observabilidad con LangSmith — 10 min  
- Mini-tareas guiadas — 40 min  
- RAG básico con FAISS — 35 min  

## Desarrollo
Comencé configurando las dependencias del entorno e integrando la API de OpenAI con LangChain usando `ChatOpenAI`.  
Luego realicé las primeras invocaciones (“Hello LLM”) para confirmar que la configuración estaba correcta.

A continuación experimenté con los parámetros de decodificación:  
probé varias combinaciones de *temperature* (0.0 / 0.5 / 0.9), *max_tokens* y *top_p*,  
observando cómo afectaban la creatividad, coherencia y determinismo del texto generado.  
**Temperature** resultó ser la variable con mayor impacto en la variabilidad del estilo.

Después trabajé con **ChatPromptTemplate**, separando instrucciones del contenido dinámico  
y componiendo el flujo mediante LCEL (`prompt | llm`).  
Esto permitió obtener prompts reutilizables, más limpios y consistentes.  
Incluso agregué un few-shot mínimo para tareas donde zero-shot no era suficientemente preciso.

Posteriormente utilicé **with_structured_output(...)** para obtener respuestas en formato JSON validado por Pydantic.  
Esto reemplaza por completo la técnica frágil de “pedir JSON por texto”,  
ya que el modelo genera directamente objetos estructurados, sin necesidad de parseo manual.

Con LangSmith habilité el tracing automático, pudiendo observar métricas de tokens, latencia y logs detallados  
de cada invocación. Esto permitió entender el costo real por llamada y cómo las plantillas más largas  
incrementan el uso de tokens.

Luego resolví mini-tareas guiadas:  
- Un **traductor determinista** con temperature=0 y salida JSON.  
- Un **resumen ejecutivo** con secciones fijas.  
- Un **Q&A con contexto limitado**, observando cuándo el modelo alucina si la información no alcanza.  
- Comparé **zero-shot vs few-shot** con ejemplos mínimos.  
- Realicé **resúmenes map-reduce** con división en chunks y consolidación final.  
- Implementé **extracción estructurada de entidades** con campos opcionales/obligatorios.  
- Finalicé con un **RAG básico** usando embeddings + FAISS para recuperar contexto antes de generar la respuesta.  

## Evidencias
https://colab.research.google.com/drive/1ENTbzvzTu0RRARnkqVmi15kY8QlpjQFV#scrollTo=m4pJxBuV4BZn

## Reflexión
Este trabajo me permitió entender a fondo cómo se construyen aplicaciones modernas basadas en LLMs utilizando LangChain  
y cómo controlar el comportamiento del modelo para obtener resultados confiables.

A continuación las reflexiones solicitadas:

### 1. Parámetros de decodificación  
Temperature fue el parámetro más determinante:  
- Con **0.0**, las respuestas fueron completamente deterministas y enfocadas.  
- Con **0.9**, apareció creatividad, pero también menor estabilidad.  
También confirmé que no conviene usar *temperature* y *top_p* altos al mismo tiempo.

### 2. Plantillas con ChatPromptTemplate  
Las plantillas mejoraron notablemente la consistencia.  
Separar instrucciones del contenido dinámico evita “drift” en el estilo del modelo.  
Agregar un único few-shot ya produce mejoras claras en clasificación y tareas sensibles a formato.

### 3. Salida estructurada  
El método **with_structured_output()** fue la parte más poderosa del assignment:  
el modelo genera directamente objetos validados por Pydantic, evitando errores comunes de formato.  
Esto es esencial para producción, donde se necesita control estricto sobre la estructura de salida.

### 4. Observabilidad  
LangSmith permitió ver tokens, latencia y las cadenas ejecutadas.  
Las trazas mostraron que prompts más largos consumen más contexto y aumentan el costo,  
y que el tiempo de inferencia varía según longitud y complejidad de los mensajes.

### 5. Zero-shot vs Few-shot  
Few-shot resultó claramente superior en tareas de clasificación y formularios estructurados.  
Zero-shot funciona, pero es menos estable y más sensible a la redacción del prompt.

### 6. Mini-tareas guiadas  
El traductor determinista mostró cómo eliminar variabilidad con temperature=0.  
En el Q&A, observé que sin suficiente contexto el modelo puede inventar datos,  
por lo que las reglas explícitas (“Si no hay suficiente contexto, devolvé X”) son obligatorias.  
El resumen map-reduce funcionó bien para textos largos, ajustando chunk_size y overlap.

### 7. RAG básico  
El RAG permitió “acotar” al modelo y evitar alucinaciones, ya que responde exclusivamente con el contexto recuperado.  
El valor de **k** influenció la calidad: k mayores incluyen más contexto pero también más tokens.

Este trabajo consolida la base para desarrollar aplicaciones más complejas con LLMs:  
prompts sólidos, salidas fiables, recuperación de documentos y observabilidad.

## Próximos pasos
Procedí a realizar la tarea de la UT4 - Agentes con LangGraph — RAG, Tools y Memoria Conversacional
