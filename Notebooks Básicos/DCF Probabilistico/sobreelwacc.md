# 🧠 Análisis del WACC (Weighted Average Cost of Capital)

El **WACC** es la tasa de descuento utilizada para traer los flujos de caja futuros al presente. Representa la rentabilidad mínima que los inversores (accionistas y acreedores) exigen por el riesgo de la empresa.

## ¿Cómo se define en este modelo?

A diferencia de un modelo estático donde se calcula un WACC fijo (ej. 10.5%), en este **DCF Probabilístico** asumimos que el WACC es una fuente de incertidumbre. En el código, el WACC se modela como una **Distribución Normal Truncada**:

### Parámetros asumidos:

1. **Media () de 12%:** Se elige un 12% como valor central por ser el estándar típico para empresas **Tech/Growth**. Estas empresas tienen betas altos (generalmente ), lo que eleva el costo del capital propio () por encima del promedio del mercado (8-9%).
2. **Desviación Estándar () de 2.5%:** Esto permite que en las 10,000 simulaciones, el WACC fluctúe mayoritariamente entre el 9.5% y el 14.5%.
3. **Límites (Truncamiento):** Se limita entre **8%** (suelo mínimo para empresas de riesgo) y **18%** (techo máximo de riesgo antes de que el negocio sea financieramente inviable).

## ¿Por qué no usamos la fórmula tradicional de CAPM?

En empresas *High-Growth* como **Snowflake (SNOW)**, el cálculo tradicional del WACC suele ser inestable debido a:

* **Betas volátiles:** La correlación con el mercado cambia rápidamente.
* **Estructura de capital cambiante:** Muchas empresas growth no tienen deuda significativa (o es deuda convertible), por lo que el WACC es casi idéntico al Costo del Equity ().
* **Riesgo de ejecución:** En estas empresas, el riesgo no es solo el mercado, sino la capacidad de escalar.

### Impacto en la Valoración

El WACC tiene una relación **inversamente proporcional** al valor de la empresa. Como se observa en el **Tornado Chart** generado por el código:

* Si el **WACC sube**, el denominador de nuestra fórmula de valor presente aumenta, lo que **desploma** el precio teórico.
* Una pequeña variación del 1% en el WACC suele tener un impacto mayor en el precio que un cambio del 1% en el crecimiento.

---

## Implementación en el Código

```python
# Así se genera en la simulación
waccs = stats.truncnorm(
    a=(0.08 - 0.12) / 0.025, # Límite inferior estandarizado
    b=(0.18 - 0.12) / 0.025, # Límite superior estandarizado
    loc=0.12, 
    scale=0.025
).rvs(n_simulaciones)

```