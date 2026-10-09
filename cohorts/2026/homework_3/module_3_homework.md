# Module 3: Teaching a Machine to Read the Market (English)

Hello! If you are a student or just starting with data analytics and financial markets, this guide is for you. Here I explain, step by step and with simple analogies, what this homework is about and how it was solved, even if you have never written a line of code.

> **Credits first:** the notebook [`Module_3_Homework_(2026_Cohort).ipynb`](./Module_3_Homework_(2026_Cohort).ipynb) is the official Module 3 Colab from the [Stock Markets Analytics Zoomcamp](https://github.com/DataTalksClub/stock-markets-analytics-zoomcamp) by DataTalksClub. All the base logic (loading the data, building the features, training the decision trees, the ARIMA example) **was already written by the course**. My work was only to solve the homework questions on top of it.

## The big question

We have **25 years of daily data for 33 of the largest stocks** in the US, Europe and India. For every day we ask one simple question:

> **Will this stock be higher in 30 days than it is today? (yes = 1, no = 0)**

To answer it we try three kinds of "fortune tellers": calendar patterns, simple hand-made rules, and a Machine Learning model called a **decision tree**.

## Key ideas (in plain words)

- **Dataset:** a giant Excel sheet. Each row is one stock on one day; each column is a piece of information about it (price, volume, technical indicators like RSI, interest rates, inflation…).
- **Train / Validation / Test:** like studying for an exam. We **study** with the oldest 85% of the data (train + validation) and take the **final exam** with the most recent 15% (test). We never mix them, because you cannot use the future to predict the past.
- **Dummy variables:** computers don't understand the word "October". So we create columns of 0s and 1s: `Month_October = 1` if the row is from October, `0` if not.
- **Correlation:** a number from -1 to 1 that tells us how much two things move together. Close to 0 means "almost no relationship".
- **Precision:** of all the times the model said *"it will go up"*, how many times was it right? A precision of 0.60 means it was right 6 times out of 10.
- **Decision tree:** a flowchart of yes/no questions that the computer learns by itself, like *"Is the 10-year interest rate below 4%? → Is the RSI above 50? → I bet it goes up"*.

## What we did, question by question

### Question 1 – Does the week of the month matter?
**Analogy:** some people say *"the market always goes up at the end of October"*. Let's check it with data.
**What we did:** for every day we created a label with the month and the week of the month (for example, the 22nd of October → `October_w4`, using the formula `(day - 1) // 7 + 1`). That label became ~60 new dummy columns. Then we measured the correlation of each one with "the stock went up in the next 30 days".
**Result:** the strongest one is **`October_w4`**, with an absolute correlation of **0.025**. Lesson: calendar effects exist, but they are **very weak** on their own.

### Question 2 – Two new "hand-made" rules
**Analogy:** a rule of thumb, like *"if interest rates are low, money flows to stocks, so I bet they go up"*.
**What we did:** we created two rules inspired by the branches of the decision tree:
- `pred3`: 10-year rate ≤ 4.5% **and** 5-year rate ≤ 4% → "goes up".
- `pred4`: 10-year rate > 4% **and** Fed rate ≤ 4.795% → "goes up".
**Result:** on the test period, `pred3` was right **58.8%** of the times it said "up" (precision **0.588**), better than `pred4` (0.503).

### Question 3 – Does the Machine Learning model add something new?
**Analogy:** if a new employee is only right when the old employees are also right, they bring nothing new to the team.
**What we did:** we trained a decision tree with 10 levels (`max_depth=10`, `random_state=42` so the result is always the same) using only past data, predicted every day of the dataset (`pred5_clf_10`), and counted the test days where **only the tree was right and all 5 hand-made rules were wrong**.
**Result:** **1,250** days. The model does find opportunities that simple rules miss.

### Question 4 – How deep should the tree be?
**Analogy:** a tree that is too shallow is like a student who only learned general rules; a tree that is too deep is like a student who memorized the practice exam and fails the real one (**overfitting**).
**What we did:** we trained trees with depth from 1 to 12 and measured the precision of each one on the test period.
**Result:** the best depth is **4**, with a precision of **0.629** (almost 63%), better than every hand-made rule and better than the depth-10 tree (0.597). Simpler can be better.

### Question 5 – What data is missing?
Almost all the economic data in the dataset is from the US, but there are also European and Indian stocks. I would add: local interest rates and inflation (ECB, Reserve Bank of India), exchange rates (EUR/USD, USD/INR), the market fear index (VIX), oil and gold prices, earnings surprises, and local indices (Euro Stoxx 50, Nifty 50). Most of them are free with `yfinance` or FRED.

## Summary of answers

| Question | Answer |
|---|---|
| Q1 – highest absolute correlation (`month_wom`) | **0.025** (`October_w4`) |
| Q2 – precision of the best new rule | **0.588** (`pred3`) |
| Q3 – test days where only the tree is right | **1250** |
| Q4 – best tree depth (1–12) | **4** (precision 0.629) |

## How to run it yourself
1. Open the notebook in Google Colab: [open in Colab](https://colab.research.google.com/github/AlejandroFloresLu/Stock-Markets-Analytics-Zoomcamp-2026/blob/main/cohorts/2026/homework_3/Module_3_Homework_%282026_Cohort%29.ipynb).
2. Click **Runtime → Run all**. The data downloads automatically from the course's Google Drive.
3. It takes about 15–25 minutes (training the trees is the slowest part).

---

# Módulo 3: Enseñándole a una máquina a leer el mercado (Español)

¡Hola! Si eres estudiante o estás empezando con el análisis de datos y los mercados financieros, esta guía es para ti. Aquí explico, paso a paso y con analogías sencillas, de qué trata esta tarea y cómo se resolvió, aunque nunca hayas escrito una línea de código.

> **Primero, los créditos:** el notebook [`Module_3_Homework_(2026_Cohort).ipynb`](./Module_3_Homework_(2026_Cohort).ipynb) es el Colab oficial del Módulo 3 del [Stock Markets Analytics Zoomcamp](https://github.com/DataTalksClub/stock-markets-analytics-zoomcamp) de DataTalksClub. Toda la lógica base (cargar los datos, construir las variables, entrenar los árboles de decisión, el ejemplo de ARIMA) **ya venía escrita por el curso**. Mi trabajo fue solo resolver las preguntas de la tarea sobre ese código.

## La gran pregunta

Tenemos **25 años de datos diarios de 33 de las acciones más grandes** de EE. UU., Europa e India. Para cada día nos hacemos una pregunta sencilla:

> **¿Esta acción va a estar más alta dentro de 30 días que hoy? (sí = 1, no = 0)**

Para responderla probamos tres tipos de "adivinos": patrones del calendario, reglas sencillas hechas a mano y un modelo de Machine Learning llamado **árbol de decisión**.

## Ideas clave (en palabras simples)

- **Dataset:** una hoja de Excel gigante. Cada fila es una acción en un día; cada columna es un dato sobre ella (precio, volumen, indicadores técnicos como el RSI, tasas de interés, inflación…).
- **Train / Validation / Test:** como estudiar para un examen. **Estudiamos** con el 85% más antiguo de los datos (train + validation) y damos el **examen final** con el 15% más reciente (test). Nunca se mezclan, porque no se vale usar el futuro para predecir el pasado.
- **Variables dummy:** la computadora no entiende la palabra "octubre". Por eso creamos columnas de 0 y 1: `Mes_Octubre = 1` si la fila es de octubre, `0` si no.
- **Correlación:** un número de -1 a 1 que dice qué tanto se mueven juntas dos cosas. Cerca de 0 significa "casi no hay relación".
- **Precisión:** de todas las veces que el modelo dijo *"va a subir"*, ¿cuántas acertó? Una precisión de 0.60 significa que acertó 6 de cada 10 veces.
- **Árbol de decisión:** un diagrama de preguntas de sí/no que la computadora aprende sola, por ejemplo: *"¿La tasa de interés a 10 años está bajo 4%? → ¿El RSI está sobre 50? → Apuesto a que sube"*.

## Qué hicimos, pregunta por pregunta

### Pregunta 1 – ¿Importa la semana del mes?
**La analogía:** hay gente que dice *"a finales de octubre el mercado siempre sube"*. Vamos a comprobarlo con datos.
**Lo que hicimos:** a cada día le pusimos una etiqueta con el mes y la semana del mes (por ejemplo, el 22 de octubre → `October_w4`, con la fórmula `(día - 1) // 7 + 1`). Esa etiqueta se convirtió en ~60 columnas dummy nuevas. Luego medimos la correlación de cada una con "la acción subió en los siguientes 30 días".
**Resultado:** la más fuerte es **`October_w4`**, con una correlación absoluta de **0.025**. Lección: los efectos del calendario existen, pero solos son **muy débiles**.

### Pregunta 2 – Dos reglas nuevas "hechas a mano"
**La analogía:** una regla práctica, como *"si las tasas de interés están bajas, el dinero se va a la bolsa, así que apuesto a que suben"*.
**Lo que hicimos:** creamos dos reglas inspiradas en las ramas del árbol de decisión:
- `pred3`: tasa a 10 años ≤ 4.5% **y** tasa a 5 años ≤ 4% → "sube".
- `pred4`: tasa a 10 años > 4% **y** tasa de la Reserva Federal ≤ 4.795% → "sube".
**Resultado:** en el período de prueba, `pred3` acertó el **58.8%** de las veces que dijo "sube" (precisión **0.588**), mejor que `pred4` (0.503).

### Pregunta 3 – ¿El modelo de Machine Learning aporta algo nuevo?
**La analogía:** si un empleado nuevo solo acierta cuando los empleados antiguos también aciertan, no le aporta nada nuevo al equipo.
**Lo que hicimos:** entrenamos un árbol de decisión de 10 niveles (`max_depth=10`, con `random_state=42` para que el resultado siempre sea el mismo) usando solo datos del pasado, predijimos todos los días del dataset (`pred5_clf_10`) y contamos los días de prueba donde **solo el árbol acertó y las 5 reglas a mano fallaron**.
**Resultado:** **1.250** días. El modelo sí encuentra oportunidades que las reglas simples no ven.

### Pregunta 4 – ¿Qué tan profundo debe ser el árbol?
**La analogía:** un árbol muy poco profundo es como un estudiante que solo aprendió reglas generales; uno demasiado profundo es como el estudiante que se memorizó el examen de práctica y falla en el real (**sobreajuste u overfitting**).
**Lo que hicimos:** entrenamos árboles con profundidad de 1 a 12 y medimos la precisión de cada uno en el período de prueba.
**Resultado:** la mejor profundidad es **4**, con una precisión de **0.629** (casi 63%), mejor que todas las reglas a mano y mejor que el árbol de profundidad 10 (0.597). A veces, más simple es mejor.

### Pregunta 5 – ¿Qué datos faltan?
Casi toda la información económica del dataset es de EE. UU., pero también hay acciones europeas e indias. Yo agregaría: tasas de interés e inflación locales (Banco Central Europeo, Banco de la Reserva de la India), tipos de cambio (EUR/USD, USD/INR), el índice del miedo del mercado (VIX), el precio del petróleo y del oro, las sorpresas en los resultados trimestrales de las empresas y los índices locales (Euro Stoxx 50, Nifty 50). La mayoría se consiguen gratis con `yfinance` o FRED.

## Resumen de respuestas

| Pregunta | Respuesta |
|---|---|
| Q1 – mayor correlación absoluta (`month_wom`) | **0.025** (`October_w4`) |
| Q2 – precisión de la mejor regla nueva | **0.588** (`pred3`) |
| Q3 – días de prueba donde solo acierta el árbol | **1250** |
| Q4 – mejor profundidad del árbol (1–12) | **4** (precisión 0.629) |

## Cómo correrlo tú mismo
1. Abre el notebook en Google Colab: [abrir en Colab](https://colab.research.google.com/github/AlejandroFloresLu/Stock-Markets-Analytics-Zoomcamp-2026/blob/main/cohorts/2026/homework_3/Module_3_Homework_%282026_Cohort%29.ipynb).
2. Haz clic en **Entorno de ejecución → Ejecutar todas**. Los datos se descargan solos desde el Google Drive del curso.
3. Tarda unos 15–25 minutos (entrenar los árboles es lo más lento).
