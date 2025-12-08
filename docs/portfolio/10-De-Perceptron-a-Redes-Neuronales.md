---
title: "Entrada 09 — Redes Neuronales: del Perceptrón al MLP"
date: 2025-10-10
---

# Entrada 10 — De Perceptron a Redes Neuronales

## Contexto
En esta práctica analizamos cómo las redes neuronales evolucionan desde el perceptrón simple hasta el modelo multicapa (MLP), explorando su capacidad para resolver problemas no lineales.  
A través de ejemplos como las compuertas lógicas AND, OR, NOT y XOR, se comprobó empíricamente qué casos puede o no resolver un perceptrón, y por qué el MLP logra superar esas limitaciones.  
También se abordaron comparaciones entre frameworks como Scikit-learn, TensorFlow, y PyTorch Lightning, entendiendo las ventajas, limitaciones y enfoques de cada uno.

## Objetivos
- Comprender por qué un perceptrón simple no puede resolver XOR.  
- Analizar el rol del bias y los pesos en compuertas lógicas AND y OR.  
- Aplicar un MLP (Multi-Layer Perceptron) con Scikit-learn para resolver XOR.  
- Diferenciar los enfoques de entrenamiento entre Scikit-learn, TensorFlow y PyTorch.  
- Identificar ventajas, desventajas y casos de uso de cada framework.  

## Actividades (con tiempos estimados)
- Revisión del código del perceptrón y análisis de la frontera de decisión — 20 min  
- Implementación de compuertas AND, OR, NOT y XOR — 25 min  
- Entrenamiento de un modelo MLP en Scikit-learn para resolver XOR — 30 min  
- Comparación conceptual de frameworks (TensorFlow, PyTorch, Lightning) — 30 min  
- Resolución de cuestionario teórico con 14 preguntas — 40 min  

## Desarrollo
Durante esta práctica se probaron distintos casos lógicos con el perceptrón básico, comprobando que solo los linealmente separables (AND, OR, NOT) pueden resolverse con una única frontera de decisión.  
Luego se implementó una red neuronal multicapa con Scikit-learn (MLPClassifier) y se verificó que el problema XOR, que no puede dividirse con una línea recta, sí puede resolverse mediante capas ocultas.  
Finalmente, se compararon las principales bibliotecas de machine learning, entendiendo cómo cada una gestiona el proceso de entrenamiento, optimización y control de parámetros.

---

### Preguntas y respuestas

**1️⃣ ¿Por qué AND, OR y NOT funcionaron pero XOR no?**  
Porque XOR no es linealmente separable, no puede dividirse con una sola línea recta. El perceptrón simple solo puede crear una frontera lineal.

---

**2️⃣ ¿Cuál es la diferencia clave entre los pesos de AND vs OR?**  
El umbral (bias). En AND, el umbral debe ser más alto; en OR, más bajo. En otras palabras, OR se activa más fácilmente que AND.

---

**3️⃣ ¿Qué otros problemas del mundo real serían como XOR?**  
Situaciones donde solo una de dos condiciones puede cumplirse:  
- Un semáforo que no puede estar en rojo y verde al mismo tiempo.  
- Un sistema de alarma que se activa por una condición u otra, pero no ambas.

---

**4️⃣ ¿Por qué sklearn MLP puede resolver XOR pero un perceptrón no?**  
Porque el MLP tiene capas ocultas que generan múltiples líneas de decisión y pueden combinarse para crear divisiones no lineales.

---

**5️⃣ ¿Cuál es la principal diferencia entre TensorFlow/Keras y sklearn MLP?**  
TensorFlow/Keras permite controlar cada detalle del entrenamiento, mientras que Scikit-learn simplifica el proceso, ideal para prototipos rápidos.

---

**6️⃣ ¿Por qué TensorFlow usa epochs y batch_size mientras sklearn MLP no?**  
Porque TensorFlow entrena en lotes (batches) y repite los pasos (epochs) para optimizar de forma flexible.  
Scikit-learn entrena todo el conjunto de datos de una sola vez.

---

**7️⃣ ¿Cuándo usarías sigmoid vs relu como función de activación?**  
- *Sigmoid:* en la capa de salida, para clasificaciones binarias.  
- *ReLU:* en capas ocultas, para mejorar el rendimiento y evitar gradientes nulos.

---

**8️⃣ ¿Qué ventaja tiene PyTorch Lightning sobre TensorFlow puro?**  
Reduce el código repetitivo, separa mejor las etapas del entrenamiento y facilita la experimentación.

---

**9️⃣ ¿Por qué PyTorch Lightning separa training_step y test_step?**  
Porque en el entrenamiento se actualizan los pesos, mientras que en la evaluación solo se calculan métricas sin modificar el modelo.

---

**🔟 ¿Qué framework elegirías para cada escenario?**  
- Prototipo rápido: **Scikit-learn**  
- Modelo en producción: **TensorFlow/Keras**  
- Investigación avanzada: **PyTorch/PyTorch Lightning**

---

**11️⃣ ¿Por qué el error “mat1 and mat2 shapes cannot be multiplied” es común en PyTorch?**  
Porque las dimensiones del dataset no coinciden con la cantidad de neuronas de entrada del modelo.

---

**12️⃣ ¿Qué significa deterministic=True en PyTorch Lightning Trainer?**  
Fuerza la reproducibilidad de resultados entre ejecuciones, fijando las semillas aleatorias.

---

**13️⃣ ¿Por qué TensorFlow muestra curvas de loss y val_loss durante entrenamiento?**  
Para visualizar posibles casos de overfitting: si la pérdida de validación aumenta mientras la de entrenamiento baja, el modelo está sobreajustando.

---

**14️⃣ ¿Cuál es la diferencia entre trainer.test() y trainer.predict() en PyTorch Lightning?**  
- `trainer.test()` calcula métricas de rendimiento.  
- `trainer.predict()` genera predicciones sin medir desempeño.

---

**15️⃣ ¿Por qué sklearn MLP es más fácil pero menos flexible?**  
Porque automatiza muchos pasos del proceso de entrenamiento, sacrificando personalización y control detallado del modelo.

---

## Evidencias
https://colab.research.google.com/drive/1CVYq5nakYt-6JPhYoUuahuVJZd2I4u-9?usp=sharing

## Reflexión
En esta práctica entendí la diferencia entre problemas lineales y no lineales, y por qué una red multicapa permite resolver los segundos.  
También comprendí cómo el bias y los pesos definen la frontera de decisión, y cómo las funciones de activación cambian el comportamiento de las neuronas.  
Finalmente, aprendí que la elección del framework depende del objetivo: rapidez, producción o investigación.

## Próximos pasos
Procederé a realizar tarea 2 de la UT2
