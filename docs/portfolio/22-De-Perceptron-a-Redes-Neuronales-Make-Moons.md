---
title: "De Perceptron a Redes Neuronales Make Moons"
date: 2025-10-13
---

# Entrada 22 De Perceptron a Redes Neuronales Make Moons

## Contexto
En esta práctica adicional exploré un dataset sintético muy utilizado para evaluar modelos clasificadores: **make_moons**, el cual presenta dos clases en forma de medias lunas entrelazadas.  
Este tipo de distribución es **no lineal**, por lo que resulta ideal para observar de manera visual y didáctica las limitaciones del perceptrón simple y, en contraste, la capacidad del **MLP** (Multi-Layer Perceptron) para aprender fronteras curvas.

La tarea consistió en generar el dataset, entrenar dos modelos distintos (Perceptrón y MLP), comparar sus fronteras de decisión y analizar por qué uno falla mientras el otro logra capturar la estructura compleja del conjunto.

## Objetivos
- Visualizar un dataset no lineal y comprender su estructura.  
- Evaluar la capacidad del perceptrón simple frente a un problema no lineal.  
- Implementar un MLP que aprenda una frontera curva.  
- Comparar la performance y las fronteras de decisión entre Perceptrón y MLP.  
- Comprender intuitivamente cómo las capas ocultas permiten resolver problemas no linealmente separables.

## Actividades (con tiempos estimados)
- Generación del dataset make_moons y visualización inicial — 10 min  
- Entrenamiento del Perceptrón y análisis de resultados — 15 min  
- Implementación del MLP con Scikit-learn — 25 min  
- Entrenamiento de una red equivalente con TensorFlow — 30 min  
- Comparación gráfica de fronteras de decisión — 20 min  
- Conclusiones y análisis conceptual — 20 min  

## Desarrollo
Comencé generando el dataset **make_moons**, agregando un nivel moderado de ruido para que el problema fuera más realista. Las dos “lunas” resultantes se superponen parcialmente, lo que hace imposible una división lineal.

Entrené primero un **Perceptrón**, observando que la frontera de decisión obtenida era completamente recta. Este modelo logró capturar parcialmente la división, pero quedó claro que no podía adaptarse a la curvatura del dataset.

Luego entrené un **MLPClassifier** de Scikit-learn con una capa oculta de 8 neuronas y activación ReLU. La frontera aprendida fue no lineal y se ajustó adecuadamente al patrón de medias lunas, alcanzando un accuracy considerablemente mayor.

Finalmente, repliqué el experimento utilizando **TensorFlow/Keras**, implementando una red con dos capas densas y entrenamiento por mini-batches. La frontera obtenida también fue curva, aunque con segmentos piecewise-linear propios de ReLU. Ajustando epochs y cantidad de neuronas se observó cómo el modelo mejora su capacidad de adaptación.

---

### Conclusiones de la práctica

**1️⃣ ¿Por qué el perceptrón falla en make_moons?**  
Porque solo puede producir **una frontera lineal**, incapaz de dividir correctamente las medias lunas entrelazadas.

---

**2️⃣ ¿Qué aporta el MLP que permite resolver el problema?**  
Sus capas ocultas generan **combinaciones no lineales** de los datos, lo que permite construir fronteras curvas mediante funciones de activación como ReLU.

---

**3️⃣ ¿Por qué make_moons es un buen dataset para este tipo de ejercicios?**  
Porque es lo suficientemente simple para visualizarlo en 2D, pero lo bastante complejo como para exigir una red neuronal multicapa.

---

**4️⃣ ¿Qué diferencia observaron entre Scikit-learn y TensorFlow?**  
- *Scikit-learn:* entrenamiento simple, ideal para probar rápido arquitecturas pequeñas.  
- *TensorFlow:* mayor control, entrenamiento por epochs, posible obtener mejores fronteras con ajustes finos.

---

**5️⃣ ¿Qué representa visualmente la frontera curva del MLP?**  
La capacidad del modelo para **doblar y deformar** el espacio de representación hasta separar ambas clases de manera óptima.

---

## Evidencias
https://colab.research.google.com/drive/1vdy9tM8Z3lWgwrWWSC9_2nGR8bT_grOk?usp=sharing
---

## Reflexión
Con esta tarea pude consolidar la diferencia entre modelos lineales y no lineales. El perceptrón, aunque útil para problemas sencillos, no puede resolver fronteras curvas.  
El MLP, en cambio, demostró que incluso con pocas neuronas ya puede captar relaciones más complejas, adaptándose al dataset y logrando una clasificación precisa.

Las visualizaciones fueron especialmente útiles para entender cómo cambia el comportamiento del modelo dependiendo de su arquitectura, y reforzaron la idea de que la profundidad y las funciones de activación expanden enormemente el espacio de soluciones posibles.

## Próximos pasos
Procedì a realizar la tarea: Segmentación de Caminos en Imágenes Satelitales con U-Net  
