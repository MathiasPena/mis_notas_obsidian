
En Pandas, **`df.info()`** y **`df.memory_usage()`** son dos métodos muy útiles para obtener información sobre el uso de memoria y los tipos de datos de un DataFrame. Estos métodos te permiten realizar un diagnóstico rápido de los datos y planificar cómo optimizar el uso de memoria.

### 5.1. **`df.info()`**

El método **`df.info()`** proporciona un resumen general del DataFrame, incluyendo el número de entradas (filas), el tipo de cada columna, el número de valores no nulos, y el uso de memoria aproximado. Es muy útil para obtener una vista rápida del estado de tus datos.

#### Ejemplo:

```python
import pandas as pd

# Crear un DataFrame de ejemplo
data = {'col1': [1, 2, 3, 4, 5], 'col2': [10.5, 20.1, 30.3, 40.4, 50.5], 'col3': ['A', 'B', 'C', 'D', 'E']}
df = pd.DataFrame(data)

# Usar df.info() para obtener información general del DataFrame
df.info()
```

Salida:
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 5 entries, 0 to 4
Data columns (total 3 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   col1    5 non-null      int64  
 1   col2    5 non-null      float64
 2   col3    5 non-null      object 
dtypes: float64(1), int64(1), object(1)
memory usage: 163.0+ bytes
```

#### Explicación:
- **Número de entradas**: 5 filas en este caso.
- **Número de valores no nulos**: 5 no nulos en cada columna, indicando que no hay datos faltantes.
- **Tipos de datos**: El DataFrame tiene columnas de tipo **int64**, **float64** y **object**.
- **Uso de memoria**: El uso de memoria total es **163.0 bytes**.

### 5.2. **`df.memory_usage()`**

El método **`df.memory_usage()`** proporciona el uso de memoria exacto por columna en el DataFrame. Esto es útil para entender cómo se distribuye el uso de memoria entre las diferentes columnas, especialmente cuando se están manejando grandes volúmenes de datos.

#### Ejemplo:

```python
# Usar df.memory_usage() para ver el uso de memoria por columna
print(df.memory_usage())
```

Salida:
```
Index     128
col1       40
col2       40
col3       80
dtype: int64
```

#### Explicación:
- Cada columna tiene un uso de memoria distinto. El índice usa **128 bytes**, mientras que las columnas **col1** y **col2** usan **40 bytes** cada una, y **col3** usa **80 bytes** (debido a ser de tipo **object**).
  
#### `df.memory_usage(deep=True)`
Si quieres obtener una estimación más precisa del uso de memoria de las columnas de tipo **object** (como las cadenas de texto), puedes usar el parámetro **deep=True** en **`memory_usage()`**. Esto calcula el uso de memoria de los objetos subyacentes (como las cadenas).

#### Ejemplo con **`deep=True`**:

```python
# Ver uso de memoria detallado con deep=True
print(df.memory_usage(deep=True))
```

Salida:
```
Index     128
col1       40
col2       40
col3      176
dtype: int64
```

#### Explicación:
- En este caso, **col3** ha aumentado su uso de memoria a **176 bytes** porque ahora se considera la memoria utilizada por las cadenas de texto.

### 5.3. **Comparación entre `df.info()` y `df.memory_usage()`**

| Método          | Información proporcionada                                    |
|-----------------|--------------------------------------------------------------|
| **`df.info()`** | Resumen general del DataFrame (número de filas, tipos de datos, número de valores no nulos, uso de memoria aproximado) |
| **`df.memory_usage()`** | Uso de memoria exacto por columna, útil para detalles finos sobre el consumo de memoria de cada columna |
| **`df.memory_usage(deep=True)`** | Proporciona el uso de memoria más preciso para columnas de tipo **object** (por ejemplo, cadenas de texto) |

### 5.4. **Conclusiones**:
- **`df.info()`** es útil para obtener una visión general rápida del DataFrame, incluyendo el tipo de datos y el uso aproximado de memoria.
- **`df.memory_usage()`** te da información detallada sobre el uso de memoria de cada columna, lo que es útil para identificar posibles optimizaciones.
- Usar **`deep=True`** en **`memory_usage()`** es esencial cuando trabajas con datos de tipo **object** (como texto) para obtener una medición precisa de la memoria.

