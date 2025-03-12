

Pandas permite crear gráficos rápidamente utilizando la función `.plot()`. Esta función es una interfaz conveniente para crear gráficos básicos como líneas, barras y más, sin necesidad de importar otras bibliotecas como Matplotlib directamente.

## Sintaxis Básica

La sintaxis general para crear un gráfico con Pandas es:

```python
df.plot(kind='tipo', x='columna_x', y='columna_y')
```

- **kind**: Especifica el tipo de gráfico (línea, barra, etc.).
- **x**: Columna del DataFrame para el eje x.
- **y**: Columna del DataFrame para el eje y.

## Tipos de Gráficos

Los principales tipos de gráficos que puedes crear son:

### 1. Gráfico de Líneas (Predeterminado)
El gráfico de líneas es el tipo por defecto al usar `.plot()`. Ideal para mostrar series temporales.

```python
import pandas as pd
import numpy as np

# Crear un DataFrame de ejemplo
df = pd.DataFrame({
    'fecha': pd.date_range(start='2021-01-01', periods=10, freq='D'),
    'valor': np.random.randn(10)
})

df.set_index('fecha').plot()
```

### 2. Gráfico de Barras

Se utiliza para mostrar la comparación entre diferentes categorías.

```python
df.plot(kind='bar', x='categoría', y='valor')
```

### 3. Gráfico de Barras Apiladas

Se usa para mostrar la comparación de valores apilados por categorías.

```python
df.plot(kind='bar', stacked=True)
```

### 4. Gráfico de Histograma

Útil para mostrar la distribución de una variable.

```python
df['valor'].plot(kind='hist', bins=10)
```

### 5. Gráfico de Dispersión (Scatter)

Ideal para mostrar la relación entre dos variables.

```python
df.plot(kind='scatter', x='columna_x', y='columna_y')
```

## Personalización del Gráfico

Pandas ofrece varias opciones para personalizar los gráficos:

### Títulos y Etiquetas

```python
ax = df.plot()
ax.set_title('Título del Gráfico')
ax.set_xlabel('Eje X')
ax.set_ylabel('Eje Y')
```

### Cambiar el Estilo de la Línea

```python
df.plot(style='--', color='red')
```

### Ajustar el Tamaño del Gráfico

```python
df.plot(figsize=(10, 6))
```

## Guardar el Gráfico

Puedes guardar el gráfico como una imagen con `.savefig()`.

```python
import matplotlib.pyplot as plt

df.plot()
plt.savefig('grafico.png')
```

## Conclusión

La función `.plot()` de Pandas es una herramienta rápida y poderosa para crear gráficos básicos directamente desde un DataFrame. Para gráficos más complejos o personalizados, es recomendable usar Matplotlib o Seaborn.
