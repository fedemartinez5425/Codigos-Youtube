
# 📈 DCF Probabilístico: Valuación de Empresas Growth con Monte Carlo

Este proyecto implementa un modelo de **Flujos de Caja Descontados (DCF)** avanzado utilizando simulaciones de **Monte Carlo** en Python. El objetivo es superar las limitaciones de la valuación tradicional (determinística) al modelar la incertidumbre inherente en empresas de alto crecimiento como **Snowflake (SNOW)**.

## 🚀 Contexto del Proyecto

La valuación tradicional suele fallar al intentar predecir el futuro con un solo número. Este proyecto resuelve ese problema tratando los *inputs* clave (crecimiento, márgenes, WACC) como **distribuciones de probabilidad** en lugar de valores fijos.

### ¿Qué es el DCF y por qué usar Monte Carlo?

* **DCF:** Un método que valora un activo basado en el valor presente de sus flujos de caja futuros.
* **El Problema:** Pequeños cambios en las suposiciones pueden llevar a variaciones drásticas en el precio ("Parálisis por Análisis").
* **La Solución:** Ejecutamos **10,000 simulaciones** aleatorias para obtener un rango de precios posibles, permitiéndonos tomar decisiones basadas en probabilidades y no en corazonadas.

---

## 🛠️ Requisitos Técnicos

El script utiliza las siguientes librerías de Python:

* `yfinance`: Obtención de datos financieros reales de Yahoo Finance.
* `pandas` & `numpy`: Procesamiento de datos y lógica matemática.
* `scipy`: Modelado de distribuciones estadísticas (Normal Truncada, Lognormal).
* `matplotlib` & `seaborn`: Visualización avanzada de datos.

```bash
pip install yfinance pandas numpy scipy matplotlib seaborn

```

---

## 📊 Estructura del Modelo

El análisis se divide en tres fases críticas:

### 1. Extracción de Datos Reales

El modelo conecta con la API de Yahoo Finance para obtener el Market Cap, ingresos actuales, deuda neta y acciones en circulación de forma automática.

### 2. El Dilema Determinístico

Se presentan dos escenarios (Optimista vs. Conservador) para demostrar cómo la valuación de una empresa *growth* puede variar hasta en un 100% dependiendo del sesgo del analista.

### 3. Simulación de Monte Carlo

Se asignan distribuciones a las variables más inciertas:

* **Revenue Growth:** Distribución Triangular (captura el rango de crecimiento esperado).
* **WACC:** Distribución Normal Truncada (representa el riesgo/tasa de descuento).
* **Múltiplo de Salida:** Distribución Lognormal (asume que los múltiplos tienden a ser positivos y tienen colas largas).

---

## 📈 Visualizaciones Incluidas

El script genera un tablero de control con 4 gráficos clave:

1. **Distribución de Precio:** Histograma con los valores más probables y comparación contra el precio actual de mercado.
2. **Percentiles de Valoración:** Gráfico de barras que muestra los precios en escenarios P10 (Pesimista), P50 (Base) y P90 (Optimista).
3. **Tornado Chart (Sensibilidad):** Identifica qué variable (WACC, Crecimiento o Múltiplo) tiene mayor impacto en el precio.
4. **Comparación vs Mercado:** Análisis visual de si la acción está sobre o subvaluada bajo el supuesto *ceteris paribus*.

---

## 🎓 Conclusiones Clave

1. **Valuación ≠ Un solo número:** El valor es una distribución.
2. **Margen de Seguridad:** Nos permite identificar si el precio de mercado está en un percentil bajo de nuestra simulación (oportunidad de compra).
3. **Honestidad Intelectual:** Al usar distribuciones, admitimos lo que no sabemos y cuantificamos el riesgo de forma científica.

---

## 📄 Licencia

Este proyecto es de código abierto. Úsalo para aprender, mejorar tus análisis financieros o como base para tus propios modelos de inversión.
