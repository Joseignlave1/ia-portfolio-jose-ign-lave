---
title: "Entrada 16 — Agentes con LangGraph: RAG, Tools y Memoria Conversacional"
date: 2025-11-15
---

# Entrada 16 — Agentes con LangGraph: RAG, Tools y Memoria Conversacional
~~

## Contexto
Este trabajo práctico se centró en el diseño y construcción de **agentes conversacionales basados en grafos** utilizando **LangGraph**, integrando modelos de OpenAI como “razonadores”, herramientas externas (tools), recuperación aumentada (RAG), y memoria conversacional ligera.  
El objetivo principal fue entender cómo orquestar LLMs y herramientas de manera controlada, predecible y extensible, utilizando grafos de estado multi-turn.

## Objetivos
- Diseñar un **estado de agente (AgentState)** adecuado para conversaciones extensas.  
- Construir un **agente en LangGraph** que use un LLM como núcleo de razonamiento.  
- Integrar **tools externas**, incluyendo un RAG minimalista y otras utilidades.  
- Encadenar reasoning ↔ tool-calling ↔ reasoning dentro de un grafo con bucles.  
- Implementar memoria ligera mediante un campo `summary` en el estado.  
- Ejecutar conversaciones multi-turn y analizar cómo evoluciona el estado.  
- Construir una **interfaz en Gradio** para probar el agente de forma interactiva.  

## Actividades (con tiempos estimados)
- Setup del entorno y prueba de LangGraph mínimo — 20 min  
- Implementación del estado del agente y memoria ligera — 25 min  
- Construcción del RAG básico y conversión en tool — 30 min  
- Implementación de tools adicionales de utilidad — 20 min  
- Integración del LLM con tools y ToolNode — 30 min  
- Armado del grafo completo assistant ↔ tools — 30 min  
- Ejecución multi-turn y depuración — 20 min  
- Desarrollo de interfaz en Gradio — 40 min  

## Desarrollo
Comencé configurando el entorno con LangGraph, LangChain y OpenAI. La primera etapa fue construir el esqueleto mínimo de un agente:  
un nodo *assistant* que recibe el estado (historial de mensajes), invoca al LLM, y produce una respuesta.

Luego extendí el **AgentState** para incluir un campo `summary`, pensado como memoria conversacional ligera.  
Esto permite mantener un resumen sintético de la conversación en vez de almacenar un historial indefinido.

A continuación construí un **RAG mínimo** utilizando FAISS como vector store:  
- Definí un pequeño corpus local.  
- Lo dividí en chunks con `RecursiveCharacterTextSplitter`.  
- Creé un `retriever` para consultar información relevante.  
- Convertí el RAG en una **tool** accesible por el LLM.

Después desarrollé herramientas adicionales, como `get_order_status` y `get_utc_time`.  
Estas permiten que el agente actúe de forma útil en escenarios pseudo-reales, simulando integración con servicios externos.

El siguiente paso fue **binde ar tools al LLM** mediante `bind_tools()`, habilitando el reasoning con tool-calling.  
El nodo assistant ahora decide si responde directamente o si debe invocar una tool.  
El nodo tools ejecuta la tool y devuelve la salida, que vuelve al nodo assistant para continuar el reasoning.

Diseñé el grafo completo utilizando **StateGraph**:  
START → assistant → (tools opcional) → assistant → END  
Este patrón de bucle permite multi-turn reasoning con herramientas.

Probé el comportamiento multi-turn y verifiqué cuándo el modelo decidía usar el RAG versus otras tools.  
Finalmente creé una interfaz en **Gradio**, mostrando:  
- historial conversacional,  
- estado actualizado del agente,  
- tools invocadas en cada turno.

Esto permitió observar claramente el funcionamiento interno del agente, el ruteo, y la evolución del estado.

## Evidencias
(Enlace al Google Colab — agregado manualmente)

## Reflexión
Este assignment fue clave para comprender cómo se construyen agentes modernos más allá de un simple LLM que responde mensajes.

### 1. Agentes como grafos
LangGraph formaliza la ejecución del agente como un grafo de nodos y transiciones.  
El reasoning deja de ser un “prompt gigante” y pasa a ser un flujo controlado donde cada componente tiene una responsabilidad específica.

### 2. Estado conversacional
Incorporar `summary` como memoria ligera ofrece ventajas prácticas:  
reduce costos, mantiene coherencia en diálogos largos y evita hacer *prompt stuffing* con un historial enorme.  
Sin embargo, también exige cuidar la privacidad y evitar incluir información sensible en el resumen.

### 3. Integración de tools
La separación reasoning ↔ tools fue una de las partes más importantes del ejercicio.  
El LLLM explica *qué quiere hacer* y las tools ejecutan acciones reales.  
Esto habilita comportamientos complejos como:  
- consultar bases de conocimiento,  
- recuperar documentos,  
- efectuar cálculos,  
- o llamar servicios externos.

### 4. RAG como herramienta reutilizable
Implementar RAG como tool confirmó que el modelo mejora su grounding al acceder a contexto relevante.  
Llamar la tool produce respuestas más precisas y evita alucinaciones.  
Sin embargo, hay que controlar la longitud del contexto devuelto para no saturar el prompt.

### 5. Conversación multi-turn
El grafo permitió mantener la coherencia entre turns, especialmente gracias al estado acumulado.  
LangGraph hace explícito dónde se almacena y cómo viaja la información, a diferencia de un simple LLM sin memory.

### 6. Interfaz en Gradio
La UI permitió probar turnos reales, ver qué tool se invoca en cada respuesta  
y validar que la arquitectura funciona incluso en escenarios de uso prolongado.

## Próximos pasos
Procedí a realizar la tarea Explorando GCloud de la UT5