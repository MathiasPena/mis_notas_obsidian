

En Pandas, los tipos de datos optimizados son útiles para mejorar el rendimiento y reducir el uso de memoria cuando trabajas con grandes volúmenes de datos. **Categorical** y **SparseDataFrame** son dos de estos tipos que pueden ser extremadamente útiles según el tipo de datos con los que estés trabajando.

### 3.1. **Categorical**

El tipo de dato **Categorical** en Pandas es una forma eficiente de representar datos que tienen un número limitado de categorías posibles. Esto es especialmente útil cuando tienes columnas con valores repetidos y limitados, como categorías, etiquetas o estados.

#### Características principales de **Categorical**:
- **Eficiencia en memoria**: Almacena los datos como enteros, mientras que las categorías se mantienen como un diccionario de valores únicos.
- **Rendimiento mejorado**: Las operaciones de comparación, búsqueda y agrupamiento son mucho más rápidas cuando se utilizan **Categoricals**.
- **Ordenable**: Permite ordenar las categorías en un orden específico (si es necesario).

#### Ejemplo de **Categorical**:
```python
import pandas as pd

# Crear un DataFrame con una columna categórica
data = {'Estado': ['Activo', 'Inactivo', 'Activo', 'Pendiente', 'Activo']}
df = pd.DataFrame(data)

# Convertir la columna 'Estado' a tipo Categorical
df['Estado'] = df['Estado'].astype('category')

# Ver los resultados
print(df['Estado'].dtype)  # Categorical
print(df['Estado'].cat.categories)  # Índice de categorías: ['Activo', 'Inactivo', 'Pendiente']
```

Salida:
```
category
Index(['Activo', 'Inactivo', 'Pendiente'], dtype='object')
```

En este ejemplo, la columna **'Estado'** se convierte en un tipo **Categorical**, lo que reduce el uso de memoria y acelera las operaciones en esa columna.

#### **Ventajas de usar Categorical**:
- Reduce el uso de memoria cuando las columnas contienen muchos valores repetidos.
- Mejora el rendimiento de las operaciones de agrupamiento, filtrado y comparación.

### 3.2. **SparseDataFrame**

El tipo **SparseDataFrame** en Pandas es útil cuando trabajas con grandes matrices dispersas (es decir, matrices que contienen una gran cantidad de ceros o valores nulos). **SparseDataFrame** almacena solo los valores no nulos, lo que permite ahorrar espacio de memoria significativamente.

#### Características principales de **SparseDataFrame**:
- **Memoria optimizada**: Solo almacena los elementos no nulos, lo que ahorra espacio cuando la mayoría de los valores son nulos o cero.
- **Compatible con operaciones estándar**: Aunque usa una representación optimizada en memoria, puedes realizar operaciones estándar como cualquier otro DataFrame.

#### Ejemplo de **SparseDataFrame**:
```python
import pandas as pd
import numpy as np

# Crear un DataFrame con muchos valores nulos
data = {'A': [1, 0, 0, 4, 0],
        'B': [0, 5, 0, 0, 0],
        'C': [0, 0, 0, 7, 0]}

df = pd.DataFrame(data)

# Convertir el DataFrame a SparseDataFrame
df_sparse = df.astype(pd.SparseDtype('float', fill_value=0))

# Ver los resultados
print(df_sparse)
print(df_sparse.sparse.density)  # Densidad de los datos (proporción de valores no nulos)
```

Salida:
```
   A  B  C
0  1  0  0
1  0  5  0
2  0  0  0
3  4  0  7
4  0  0  0

Densidad: 0.2 (20% de los valores son no nulos)
```

#### **Ventajas de usar SparseDataFrame**:
- **Ahorro de memoria**: Es ideal para datos dispersos, donde muchos valores son cero o nulos, como en matrices de términos en modelos de texto o datos de sensores.
- **Eficiencia en operaciones**: Aunque los datos son almacenados de forma eficiente, puedes seguir utilizando operaciones estándar de Pandas.

### 3.3. **Cuándo usar Categorical vs SparseDataFrame**

- **Categorical** es ideal para columnas con un número limitado de valores repetidos (como categorías, estados o etiquetas).
- **SparseDataFrame** es útil cuando trabajas con grandes volúmenes de datos que contienen muchos ceros o valores nulos, como en matrices dispersas.

---

### Resumen

- **Categorical** es útil para columnas con valores repetidos y limitados. Mejora la memoria y el rendimiento.
- **SparseDataFrame** es ideal para matrices grandes y dispersas, donde la mayoría de los valores son ceros o nulos.

