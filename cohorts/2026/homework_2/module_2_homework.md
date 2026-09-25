# Módulo 2: Limpieza de Datos y Análisis Cuantitativo (Español)

¡Hola! Si eres estudiante (como de quinto semestre) o estás empezando a aprender sobre análisis de datos y mercados financieros, esta guía es para ti. Aquí te explico exactamente qué hicimos en esta tarea, usando analogías sencillas para que todo quede súper claro, sin términos extremadamente técnicos.

## ¿Qué herramientas usamos y por qué?

Imagina que estamos construyendo una casa. Necesitamos diferentes herramientas para distintas partes del proceso:

- **Python:** Es como el terreno o el lenguaje principal en el que nos comunicamos para dar instrucciones a la computadora.
- **Pandas:** Es nuestro organizador de cajas. Cuando descargas muchos datos financieros, vienen desordenados. Pandas nos ayuda a meterlos en tablas (como si fueran hojas de Excel con superpoderes) para ordenarlos, cruzarlos y filtrarlos fácilmente.
- **Numpy:** Es nuestra calculadora científica ultrarrápida. Nos sirve para hacer operaciones matemáticas con muchísimos números al mismo tiempo, sin que la computadora se quede "pensando" por horas.
- **PyArrow:** Es como un camión de mudanzas de alta velocidad. Cuando tenemos archivos gigantescos, PyArrow los lee y los guarda rapidísimo en un formato que ocupa menos espacio.
- **yfinance:** Es nuestro "chismoso" financiero. En lugar de ir a la bolsa de valores a preguntar los precios, esta herramienta se conecta directamente a Yahoo Finance y nos trae toda la información de las acciones a nuestra computadora.

## ¿Qué problemas resolvimos? (Los retos)

### 1. Limpieza de Datos de IPOs (Ofertas Públicas Iniciales)
**La analogía:** Imagina que recibes un montón de formularios llenados a mano por distintas personas. Algunos tienen manchas de café, otros están incompletos y algunos tienen datos absurdos.
**Lo que hicimos:** Tomamos un conjunto de datos sobre empresas que están saliendo a la bolsa (IPOs). Usamos nuestras herramientas para quitar "la basura", arreglar los espacios vacíos y asegurarnos de que la información fuera 100% confiable antes de hacer cálculos con ella.

### 2. Cálculo del Índice de Sharpe
**La analogía:** Imagina dos inversiones. La Inversión A te da un 10% de ganancia segura en una cuenta de ahorros. La Inversión B te da un 12%, pero es un negocio arriesgado donde a veces pierdes dinero. ¿Cuál es mejor?
**Lo que hicimos:** Calculamos el Índice de Sharpe. Esta fórmula nos dice si esa ganancia extra vale la pena frente al riesgo de perder el dinero. Nos ayuda a saber si estamos tomando un "riesgo inteligente" o si solo estamos apostando a ciegas.

### 3. Simulación de Trading usando el RSI (Índice de Fuerza Relativa)
**La analogía:** Imagina un resorte. Si lo estiras mucho (acciones muy caras o sobrecompradas), eventualmente va a rebotar hacia abajo con fuerza. Si lo comprimes mucho (acciones muy baratas o sobrevendidas), va a rebotar hacia arriba.
**Lo que hicimos:** Usamos un indicador llamado RSI que actúa como un medidor de tensión para ese resorte. Creamos una simulación de código que "compra" cuando el resorte está muy comprimido (una oportunidad) y "vende" cuando está muy estirado. Así probamos si esta estrategia nos haría ganar dinero en la vida real.

---

# Module 2: Data Cleaning and Quantitative Analysis (English)

Hello! If you are a student (like in your 5th semester) or just starting to learn about data analytics and financial markets, this guide is for you. Here, I explain exactly what we did in this homework using simple analogies so everything is super clear, without overly technical jargon.

## What tools did we use and why?

Imagine we are building a house. We need different tools for different parts of the process:

- **Python:** It's like the land or the main language we use to give instructions to the computer.
- **Pandas:** It's our box organizer. When you download a lot of financial data, it comes messy. Pandas helps us put it into tables (like Excel sheets with superpowers) to sort, cross-reference, and filter them easily.
- **Numpy:** It's our ultra-fast scientific calculator. It helps us do mathematical operations with huge amounts of numbers at the same time, without the computer getting stuck "thinking" for hours.
- **PyArrow:** It's like a high-speed moving truck. When we have gigantic files, PyArrow reads and saves them very quickly in a format that takes up less space.
- **yfinance:** It's our financial "gossiper". Instead of going to the stock exchange to ask for prices, this tool connects directly to Yahoo Finance and brings all the stock information right to our computer.

## What problems did we solve? (The challenges)

### 1. Data Cleaning of IPOs (Initial Public Offerings)
**The analogy:** Imagine you receive a bunch of forms filled out by hand by different people. Some have coffee stains, others are incomplete, and some have absurd data.
**What we did:** We took a dataset about companies going public (IPOs). We used our tools to remove the "trash", fix the empty spaces, and make sure the information was 100% reliable before running calculations on it.

### 2. Sharpe Ratio Calculation
**The analogy:** Imagine two investments. Investment A gives you a guaranteed 10% profit in a savings account. Investment B gives you 12%, but it's a risky business where you sometimes lose money. Which one is better?
**What we did:** We calculated the Sharpe Ratio. This formula tells us if that extra profit is worth the risk of losing money. It helps us know if we are taking a "smart risk" or just betting blindly.

### 3. Trading Simulation using the RSI (Relative Strength Index)
**The analogy:** Imagine a spring. If you stretch it too much (stocks that are too expensive or overbought), it will eventually bounce back down hard. If you compress it too much (stocks that are too cheap or oversold), it will bounce back up.
**What we did:** We used an indicator called RSI that acts as a tension meter for that spring. We created a code simulation that "buys" when the spring is too compressed (an opportunity) and "sells" when it's too stretched. This way we tested if this strategy would make us money in real life.
