# Cálculo de Diferencias en Pandas: `diff()`, `pct_change()`

Las funciones **`diff()`** y **`pct_change()`** en **Pandas** se utilizan para calcular las diferencias entre elementos consecutivos en una serie o DataFrame, lo que resulta útil en el análisis de series temporales y para medir variaciones en los datos.

## **1. `diff()`**: Diferencias entre Elementos Consecutivos

La función **`diff()`** calcula la diferencia entre un valor y el valor anterior, lo que es útil para detectar cambios en los datos de una serie temporal.

### Ejemplo: Calcular las Diferencias

```python
import pandas as pd

# Crear un DataFrame de ejemplo
data = {'fecha': pd.date_range('2021-01-01', periods=5, freq='D'),
        'valor': [100, 200, 300, 250, 500]}
df = pd.DataFrame(data)

# Calcular las diferencias
df['diferencia'] = df['valor'].diff()

print(df)
```

Este ejemplo calcula las diferencias entre los valores consecutivos de la columna **`valor`**. El primer valor de la columna **`diferencia`** será `NaN` ya que no tiene un valor anterior con el cual calcular la diferencia.

### Argumentos de `diff()`:
- **`periods`**: El número de períodos a desplazar. Por defecto es 1, pero puedes cambiarlo para calcular diferencias a mayor distancia.
- **`axis`**: El eje en el que calcular las diferencias. 0 para filas y 1 para columnas.

## **2. `pct_change()`**: Cambio Porcentual entre Elementos Consecutivos

La función **`pct_change()`** calcula el cambio porcentual entre un valor y el valor anterior. Esto es útil cuando deseas medir las variaciones relativas, en lugar de las absolutas.

### Ejemplo: Calcular el Cambio Porcentual

```python
# Calcular el cambio porcentual
df['cambio_porcentual'] = df['valor'].pct_change() * 100  # Multiplicamos por 100 para obtener el porcentaje

print(df)
```

Este ejemplo calcula el cambio porcentual entre los valores consecutivos de la columna **`valor`**. Al igual que con **`diff()`**, el primer valor será `NaN` ya que no hay un valor anterior para calcular el cambio porcentual.

### Argumentos de `pct_change()`:
- **`periods`**: El número de períodos a desplazar para calcular el cambio. El valor por defecto es 1.
- **`fill_method`**: Define cómo manejar los valores `NaN` en el cálculo. Puede ser `pad` (rellenar con el valor anterior) o `bfill` (rellenar con el siguiente valor).
- **`limit`**: Límite del número de valores `NaN` que se rellenan.
- **`freq`**: Si se trabaja con series temporales, puedes especificar la frecuencia de la serie para el cálculo.

## **Conclusión**:

- **`diff()`** es útil para calcular diferencias absolutas entre valores consecutivos, ayudando a detectar cambios directos entre datos.
- **`pct_change()`** es útil para calcular el cambio porcentual entre valores consecutivos, proporcionando una medida relativa del cambio.

Ambas funciones son ampliamente utilizadas en análisis de series temporales, análisis financiero, y cuando necesitamos comparar valores en el tiempo.
