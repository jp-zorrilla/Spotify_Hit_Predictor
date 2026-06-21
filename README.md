# Spotify_Hit_Predictor: Aplicando IA a la Industria Musical

Este proyecto responde a la pregunta de si una canción puede llegar a ser un *Hit* solo por como suena a través de un pipeline de Machine Learning de extremo a extremo. El objetivo no fue buscar el algoritmo más complejo del mercado, sino construir una herramienta real, interpretable y con viabilidad económica para discográficas y plataformas de streaming.

Este repositorio  encontrarás el análisis completo, el desarrollo del modelo predictivo y la conexión con un Dashboard Ejecutivo interactivo.
_ _ _

## 📌 El Problema de Negocio: ¿Qué hace que una canción sea un Hit?

En la era del streaming, miles de canciones se suben a diario. Esto podría significar para una firma discográfica, invertir a ciegas en campañas de marketing, lo que implicaría un riesgo financiero enorme. Este proyecto busca mitigar ese riesgo identificando que hace que una canción sea un *Hit* antes  de que exploten en las plataformas, permitiendo una asignación de presupuesto mucho más inteligente (algo que podríamos llamar como un *ADN acústico/musical*).
_ _ _

## 📊 El Dataset

Trabajamos con un volumen final de **81,343 canciones únicas** extraídas directamente de la API de Spotify. El análisis incluye características acústicas clave como:
* `danceability` (Qué tan bailable es)
* `energy` (Intensidad y actividad)
* `valence` (La positividad musical que transmite)
* `duration_min` (Duración real del track, calculada mediante ingeniería de variables)

El objetivo (*Target*) fue clasificar los temas en **Hit (1)** o **Flop (0)** basándonos en un umbral histórico de popularidad.

---

## 🚨 El Desafío Técnico: Cazando el "Data Leakage"

Uno de los aprendizajes más valiosos de este proyecto ocurrió durante la fase de modelado. En la primera iteración, un modelo de *Random Forest* arrojaba un rendimiento falsamente perfecto. Tras revisar el código, encontramos un problema de **Data Leakage**: el algoritmo estaba utilizando la columna oculta `Unnamed: 0` (el índice automático del archivo) para memorizar la posición física de las filas en lugar de aprender música.

**La solución:** Eliminamos esta variable de control. Esto forzó a los algoritmos a competir procesando únicamente los atributos musicales, logrando un modelo verdaderamente honesto y aplicable al mundo real.

---

## 🥊 Modelado y Resultados

Tras corregir el sesgo de los datos y balancear las clases (`class_weight='balanced'`), enfrentamos a una **Regresión Logística** contra un **Random Forest**:

| Métrica | Regresión Logística (Ganador) | Random Forest (Challenger) |
| :--- | :---: | :---: |
| **Accuracy General** | **75%** | 66% |
| **Recall (Detección de Hits)** | **80%** | 78% |
| **Precisión (Certeza de Hits)** | **49%** | 41% |

### Conclusión del Modelo:
Siguiendo el principio de simplicidad, **la Regresión Logística fue superior al Random Forest**. 
* El **Recall del 80%** es lamétrica clave para el negocio: significa que de cada 100 éxitos reales del mercado, el algoritmo logra capturar 80, reduciendo al mínimo el riesgo de dejar pasar un talento masivo.
* Además, su costo computacional de despliegue es nulo y ofrece una interpretabilidad matemática absoluta frente a los directivos.

---

## 🎨 Dashboard Ejecutivo en Tableau

Para que los resultados de la IA no se queden atrapados en un cuaderno de código, exportamos las predicciones revirtiendo el escalado matemático (`inverse_transform`) para quienes gusten, puedan leer minutos reales y BPMs legibles.

Diseñamos un Dashboard interactivo en **Dark Mode** con los tres pilares estratégicos de la investigación:
1. **Rendimiento por Género:** Un panorama macro para identificar en qué nichos del mercado se concentran los éxitos.
2. **El ADN Musical:** Comparativa visual de las características acústicas promedio de los éxitos frente al resto de canciones.
3. **El Factor Duración:** Un gráfico de dispersión que valida nuestra hipótesis: la probabilidad de éxito decae drásticamente cuando una canción supera la barrera de los 4 minutos (el formato clásico de radio).

👉 **[https://public.tableau.com/app/profile/juan.pedro4173/viz/Spotify_Hits_Prediction/Anlisis_Predectivo]** 

---

## 🛠️ Tecnologías Utilizadas

* **Python** (Pandas, NumPy, Scikit-Learn, Seaborn)
* **Tableau Desktop / Public**
* **Google Colab** & Google Drive para el almacenamiento del pipeline.

---
*Proyecto de Analítica Avanzada enfocado en el impacto financiero y de negocio.*
