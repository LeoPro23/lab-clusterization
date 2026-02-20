# WORKSHOP 03: "Definiendo tipo de ML a aplicar"

## 1. Objetivo
Identificar el tipo de ML que aplicará en su proyecto

**Problema General:**
Un estudio realizado por la Organización Panamericana de la Salud, para las Américas indica que los accidentes representan el aspecto más evidente del problema, sin embargo, las enfermedades laborales constituyen el 80% de las muertes relacionadas con el trabajo. Además, se calcula que cada año ocurren existen nueve millones de accidentes y enfermedades laborales no mortales. Por otro lado, indica que estos accidentes y enfermedades son, en su mayoría, prevenibles, siempre que se desarrollen programas de seguridad de manera preventiva (OPS, 2023).

---

## 2. Desarrollo de Instrucciones

### a. Definir una problemática orientada a reducir accidentes laborales, identificando las variables respectivas.

**Problema Definido:**
A pesar de que la mayoría de los accidentes laborales son prevenibles, la falta de identificación temprana de situaciones de riesgo impide aplicar los programas preventivos de manera oportuna.
El problema a resolver con Machine Learning es: **Predecir el nivel de gravedad de un accidente laboral en instalaciones industriales basándose en las condiciones del entorno, el tipo de riesgo y el perfil del trabajador involucrado**. Esto permitirá a las empresas focalizar sus prioridades preventivas en los sectores y perfiles de mayor riesgo probabilístico.

**Identificación de Variables:**

*   **Variables Independientes (Características o Features - X):**
    *   `Industry Sector`: Sector industrial de la planta (Minería, Metalurgia, etc.).
    *   `Genre`: Género del trabajador (Masculino / Femenino).
    *   `Employee ou Terceiro`: Si es empleado directo ('Employee') o un contratista/tercero ('Third Party').
    *   `Risco Critico`: Tipo de riesgo crítico al que estaba expuesto (ej. Trabajo en altura, espacios confinados, riesgo eléctrico, entre otros).
    *   `Local` / `Countries`: Ubicación y país de la planta donde ocurre la incidencia.
*   **Variable Dependiente (Objetivo o Target - Y):**
    *   `Accident Level`: Nivel de gravedad del accidente, clasificado numéricamente en números romanos desde Nivel I (Leve) hasta Nivel VI (Catastrófico o Mortal).

### b. Incluya una muestra del dataset de trabajo (incluir link desde donde obtendrá la información).

Para este proyecto, utilizaremos un conjunto de datos real de incidentes de seguridad laboral industrial proveniente de múltiples plantas en diferentes países y sectores.

*   **Nombre del Dataset:** Industrial Safety and Health Analytics Database
*   **Link de obtención (Kaggle):** [https://www.kaggle.com/datasets/ihmstefanini/industrial-safety-and-health-analytics-database](https://www.kaggle.com/datasets/ihmstefanini/industrial-safety-and-health-analytics-database)

**Muestra del Dataset (Primeras 5 filas):**

| Data | Countries | Local | Industry Sector | Accident Level (Target) | Potential Accident Level | Genre | Employee ou Terceiro | Risco Critico |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2016-01-01 00:00:00 | Country_01 | Local_01 | Mining | I | IV | Male | Third Party | Pressed |
| 2016-01-02 00:00:00 | Country_02 | Local_02 | Mining | I | IV | Male | Employee | Pressurized Systems |
| 2016-01-06 00:00:00 | Country_01 | Local_03 | Mining | I | III | Male | Third Party (Remote) | Manual Tools |
| 2016-01-08 00:00:00 | Country_01 | Local_04 | Mining | I | I | Male | Third Party | Others |
| 2016-01-10 00:00:00 | Country_01 | Local_04 | Mining | IV | IV | Male | Third Party | Others |

### c. Determinar el tipo de algoritmo a realizar.

Dado que tenemos un conjunto de datos históricos que ya incluye las respuestas correctas etiquetadas (sabemos qué nivel de accidente numérico ocurrió en cada caso registrado históricamente), el enfoque adecuado es el **Aprendizaje Supervisado (Supervised Learning)**.

Específicamente, como nuestra variable objetivo (`Accident Level`) se divide en categorías discretas y finitas (Niveles I, II, III, IV, V, VI), el tipo de tarea principal a aplicar es la **Clasificación**.

### d. Aplique 2 algoritmos para solucionar el problema.

Para resolver este problema clasificatorio (predecir a qué categoría de "Nivel de Accidente" pertenece un incidente dado su contexto), hemos aplicado dos modelos de clasificación distintos en el notebook provisto:

1.  **Algoritmo de Bosques Aleatorios (Random Forest Classifier)**
    *   **¿Por qué aplicarlo?** Es excelente para manejar bases de datos con múltiples variables categóricas complejas (como el sector o el tipo de riesgo) sin necesidad de transformaciones matemáticas o normalizaciones exigentes. Al crear múltiples "árboles de decisión" paralelos y promediar sus resultados, evita el sobreajuste y nos indica de forma robusta qué factores o interacciones elevan más el peligro.
2.  **Regresión Logística Multinomial (Logistic Regression)**
    *   **¿Por qué aplicarlo?** A pesar de llevar la palabra "Regresión" en su nombre estadístico, es un algoritmo estándar de Clasificación (Multinomial en este caso por tener más de 2 categorías). Es ideal para establecer un modelo probabilístico base explicativo, calculando mediante una curva logística qué tan probable matemáticamente es que un conjunto de condiciones categóricas resulte en un Nivel I, II, o IV.

*(Revise el notebook de Google Colab `workshop_03.ipynb` adjunto al repositorio para observar la limpieza de datos, el codificador 'One-Hot' utilizado para variables categóricas, y el entrenamiento en Python de estos dos estimadores en la librería `scikit-learn`.)*
