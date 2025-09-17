# Mini Proyecto 1: Análisis y Predicción de Deserción Estudiantil con K-NN

## Descripción General

Este proyecto utiliza el algoritmo K-Nearest Neighbors (K-NN) para predecir la deserción de estudiantes y su rendimiento académico, basándose en un conjunto de datos que incluye información académica, demográfica y socioeconómica.

El objetivo principal es doble:
1.  **Clasificación:** Predecir si un estudiante abandonará (Dropout) o permanecerá inscrito (Enrolled).
2.  **Regresión:** Estimar la calificación promedio general de un estudiante.

## Metodología

El proyecto se desarrolla en las siguientes fases:

### 1. Carga y Limpieza de Datos

- Se cargó un conjunto de datos de `datos_miniproyecto1.csv`.
- Se renombraron las columnas para facilitar su manejo (e.g., `Target` a `Estado`).
- Se filtraron los datos para excluir a los estudiantes ya graduados (`Graduate`), enfocando el análisis en la deserción y la permanencia.
- La variable objetivo `Estado` se codificó numéricamente: `Dropout` como `0` y `Enrolled` como `1`.

### 2. Ingeniería de Características

Se crearon nuevas variables para mejorar el poder predictivo de los modelos:
- `overall_grade_avg`: Promedio de las calificaciones del primer y segundo semestre.
- `grade_change`: Diferencia entre las calificaciones del segundo y primer semestre.

### 3. Análisis Exploratorio de Datos (EDA)

Se realizó un análisis exhaustivo para entender la relación entre las variables predictoras y las variables objetivo (`Estado` y `overall_grade_avg`).

#### Hallazgos Clave para la Predicción del `Estado`:

- **Factores Económicos:** El estado de la matrícula (`Tuition fees up to date`) y si el estudiante es becado (`Scholarship holder`) mostraron ser los predictores más fuertes.
- **Factores Académicos:** El curso (`Course`) y el rendimiento en semestres anteriores también resultaron ser significativos.
- **Indicadores de Riesgo:** Ser deudor (`Debtor`) está fuertemente asociado con una mayor probabilidad de deserción.

#### Hallazgos Clave para la Predicción de `overall_grade_avg`:

- Las variables más influyentes fueron las unidades curriculares aprobadas y las calificaciones obtenidas en los semestres previos, indicando que el rendimiento pasado es el mejor predictor del rendimiento futuro.

### 4. Preprocesamiento

- **División de Datos:** El conjunto de datos se dividió en un 70% para entrenamiento y un 30% para prueba.
- **Escalado y Codificación:** Se aplicó `StandardScaler` a las variables numéricas y `OneHotEncoder` a las categóricas para asegurar que todas las características contribuyeran de manera equitativa al modelo K-NN.

### 5. Modelado

#### K-NN Clasificador

- Se entrenó un modelo K-NN para clasificar a los estudiantes como `Dropout` o `Enrolled`.
- Se optimizó el número de vecinos (`k`) utilizando la métrica de `Accuracy` balanceado, encontrando que `k=6` era el valor óptimo.
- El modelo final alcanzó un **F1-score de 0.50** y un **ROC AUC de 0.71**.

#### K-NN Regresión

- Se desarrolló un modelo para predecir la calificación promedio (`overall_grade_avg`).
- Se identificó un `k` óptimo de **24** para minimizar el Error Cuadrático Medio (RMSE).
- El modelo final obtuvo las siguientes métricas de evaluación:
    - **Error Absoluto Medio (MAE):** 2.60
    - **Raíz del Error Cuadrático Medio (RMSE):** 3.76
    - **Coeficiente de Determinación (R²):** 0.52

## Conclusiones

- El modelo de clasificación K-NN demostró ser moderadamente efectivo para predecir la deserción, aunque su rendimiento se vio afectado por el desbalance de clases.
- El modelo de regresión fue capaz de explicar aproximadamente el 52% de la variabilidad en las calificaciones promedio de los estudiantes, mostrando que el rendimiento académico previo es un predictor clave.
- Los factores económicos, como tener la matrícula al día y ser becado, son determinantes para la permanencia de los estudiantes.

## Autores

- José Menco
- Camilo Vargas
- Iván Ramirez
