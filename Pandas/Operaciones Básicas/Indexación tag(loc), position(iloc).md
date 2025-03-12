

En Pandas, existen dos métodos clave para acceder y seleccionar datos en un **DataFrame** o **Serie**: **`.loc[]`** y **`.iloc[]`**. Aunque ambos sirven para acceder a los datos, su funcionamiento y el tipo de índice con el que trabajan son diferentes.

### 2.1. **`.loc[]` - Indexación basada en etiquetas**

El **`.loc[]`** se utiliza para acceder a un grupo de filas y columnas por medio de sus **etiquetas de índice** (nombres de las filas y columnas). Es decir, puedes seleccionar los datos especificando las etiquetas de las filas y las columnas, no la posición.

#### Características principales de `.loc[]`:
- **Basado en etiquetas**: Utiliza las etiquetas del índice y las columnas, no las posiciones numéricas.
- **Inclusivo**: Al seleccionar rangos, incluye tanto el inicio como el final del rango (si existe).
  
#### Ejemplo:
```python
import pandas as pd

# Crear un DataFrame
data = {'Columna1': [10, 20, 30, 40],
        'Columna2': ['A', 'B', 'C', 'D']}
df = pd.DataFrame(data, index=['a', 'b', 'c', 'd'])

# Seleccionar una fila por su etiqueta
print(df.loc['b'])

# Seleccionar un rango de filas y columnas por etiquetas
print(df.loc['a':'c', 'Columna1'])
```

Salida:
```
Columna1    20
Columna2      B
Name: b, dtype: object

a    10
b    20
c    30
Name: Columna1, dtype: int64
```

En este ejemplo:
- **`df.loc['b']`** accede a la fila con la etiqueta `'b'`.
- **`df.loc['a':'c', 'Columna1']`** selecciona el rango de filas de 'a' a 'c' para la columna `'Columna1'`.

### 2.2. **`.iloc[]` - Indexación basada en posición**

El **`.iloc[]`** se utiliza para seleccionar filas y columnas por sus **índices de posición**. Funciona con enteros, es decir, la posición numérica de las filas y columnas en lugar de las etiquetas.

#### Características principales de `.iloc[]`:
- **Basado en posición**: Utiliza la posición numérica de las filas y columnas (empezando desde 0).
- **Exclusivo**: Al seleccionar rangos, excluye el último valor del rango (similar a cómo funcionan los índices en las listas de Python).

#### Ejemplo:
```python
import pandas as pd

# Crear un DataFrame
data = {'Columna1': [10, 20, 30, 40],
        'Columna2': ['A', 'B', 'C', 'D']}
df = pd.DataFrame(data)

# Seleccionar una fila por su posición
print(df.iloc[1])

# Seleccionar un rango de filas y columnas por posición
print(df.iloc[0:3, 0])
```

Salida:
```
Columna1    20
Columna2      B
Name: 1, dtype: object

0    10
1    20
2    30
Name: Columna1, dtype: int64
```

En este ejemplo:
- **`df.iloc[1]`** accede a la fila en la posición 1 (segunda fila).
- **`df.iloc[0:3, 0]`** selecciona las filas 0, 1 y 2 de la columna en la posición 0 (`'Columna1'`).

### 2.3. **Diferencias clave entre `.loc[]` y `.iloc[]`**

| Característica         | `.loc[]`                                | `.iloc[]`                                   |
|------------------------|-----------------------------------------|---------------------------------------------|
| **Tipo de índice**      | Basado en etiquetas (índice de filas y columnas) | Basado en posiciones numéricas (índices enteros) |
| **Inclusividad del rango** | Incluye el valor final del rango | Excluye el valor final del rango           |
| **Acceso a filas/columnas** | `df.loc[filas, columnas]` | `df.iloc[filas, columnas]`                 |
| **Acepta valores no enteros** | Sí, acepta cualquier valor de índice | Solo acepta enteros o listas de enteros    |

### 2.4. **Casos prácticos**

#### 2.4.1. **Acceder a una fila por su índice (etiqueta) o posición**
```python
# Acceder a la fila con índice 'b' usando .loc[]
print(df.loc['b'])

# Acceder a la fila en la posición 1 usando .iloc[]
print(df.iloc[1])
```

#### 2.4.2. **Seleccionar un rango de filas y columnas**
```python
# Seleccionar filas 'a' a 'c' para la columna 'Columna1' usando .loc[]
print(df.loc['a':'c', 'Columna1'])

# Seleccionar las filas 0 a 2 para la columna en la posición 0 usando .iloc[]
print(df.iloc[0:3, 0])
```

---

### Resumen

- **`.loc[]`** se utiliza cuando deseas acceder a los datos utilizando **etiquetas** de las filas y columnas.
- **`.iloc[]`** se utiliza cuando deseas acceder a los datos utilizando **posiciones numéricas**.
- Ambos métodos son potentes, pero se deben elegir según si estás trabajando con las etiquetas o las posiciones de las filas y columnas.

