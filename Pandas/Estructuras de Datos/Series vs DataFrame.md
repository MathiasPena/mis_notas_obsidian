# Pandas - Internals y Optimización

## 1. Estructura de DataFrames y Series

### 1.1. **Diferencia entre Series y DataFrame**

En Pandas, **Series** y **DataFrame** son dos de las estructuras de datos fundamentales. Ambas se utilizan para almacenar y manipular datos, pero tienen diferencias clave:

#### 1.1.1. **Series**
Una **Series** es una estructura unidimensional que puede contener cualquier tipo de dato (enteros, cadenas, flotantes, objetos, etc.). Es similar a un arreglo de una sola columna de datos, pero con un índice asociado que permite acceder a los elementos por etiqueta en lugar de solo por posición.

- **Tipo**: 1D (unidimensional)
- **Índice**: Etiquetas que pueden ser personalizadas o por defecto (0, 1, 2, ...)
- **Uso principal**: Almacenar una columna de un conjunto de datos o cualquier lista de datos con un índice.

**Ejemplo de Series**:
```python
import pandas as pd

# Crear una Serie
s = pd.Series([10, 20, 30, 40], index=['a', 'b', 'c', 'd'])
print(s)
```

Salida:
```
a    10
b    20
c    30
d    40
dtype: int64
```

#### 1.1.2. **DataFrame**
Un **DataFrame** es una estructura bidimensional (2D) que puede contener múltiples columnas, y cada columna puede ser de un tipo diferente de dato. Los **DataFrames** son el tipo de dato más utilizado en Pandas para representar tablas de datos, donde cada columna es una Serie.

- **Tipo**: 2D (bidimensional)
- **Índice**: Puede tener etiquetas para filas y columnas.
- **Uso principal**: Almacenar y manipular datos tabulares, como una tabla en una base de datos.

**Ejemplo de DataFrame**:
```python
import pandas as pd

# Crear un DataFrame
data = {'Columna1': [10, 20, 30, 40],
        'Columna2': ['A', 'B', 'C', 'D']}
df = pd.DataFrame(data)
print(df)
```

Salida:
```
   Columna1 Columna2
0        10        A
1        20        B
2        30        C
3        40        D
```

#### 1.1.3. **Diferencias clave**:

- **Estructura**: Una Serie es una sola columna, mientras que un DataFrame es una tabla de múltiples columnas.
- **Acceso a los datos**: En una Serie, los elementos son accedidos mediante el índice, mientras que en un DataFrame se accede a los datos por nombre de columna y/o índice de fila.
- **Funciones**: Ambos tienen muchas funciones similares (como `head()`, `tail()`, `describe()`), pero el DataFrame tiene funciones adicionales como `groupby()`, `merge()`, `pivot_table()`, etc., que permiten manipular múltiples columnas de manera más avanzada.

### 1.2. **Consideraciones de Optimización en Pandas**

Para trabajar de manera eficiente con grandes conjuntos de datos en Pandas, es importante entender algunas optimizaciones que puedes hacer para mejorar el rendimiento:

#### 1.2.1. **Uso de tipos de datos adecuados**

Pandas permite especificar el tipo de datos para cada columna. El uso adecuado de tipos de datos puede reducir considerablemente el uso de memoria y mejorar la eficiencia de las operaciones.

- **Categorical**: Si tienes una columna con un número limitado de valores únicos (por ejemplo, una columna de "sexo" con solo "masculino" y "femenino"), puedes convertirla en un tipo **`Categorical`**. Esto ahorra memoria y mejora el rendimiento.
  
```python
df['Sexo'] = df['Sexo'].astype('category')
```

#### 1.2.2. **Optimización de operaciones con `apply()`**

En lugar de utilizar `apply()` para operaciones complejas en DataFrames, intenta usar operaciones vectorizadas que Pandas proporciona internamente, ya que son mucho más rápidas.

**Malo (Usando `apply()` con una función Python pura)**:
```python
df['Columna3'] = df['Columna1'].apply(lambda x: x * 2)
```

**Bueno (Operación vectorizada)**:
```python
df['Columna3'] = df['Columna1'] * 2
```

Las operaciones vectorizadas son mucho más rápidas porque están optimizadas en C y evitan la sobrecarga de llamar a una función externa para cada fila.

#### 1.2.3. **Uso eficiente de `concat()` y `merge()`**

Cuando trabajes con grandes conjuntos de datos, es importante usar las funciones **`concat()`** y **`merge()`** de manera eficiente para evitar copias innecesarias de los datos.

Por ejemplo, en lugar de concatenar múltiples DataFrames dentro de un bucle, es más eficiente acumular las partes en una lista y luego concatenarlas de una vez:

```python
# Ineficiente (concatenando dentro del bucle)
for df_part in df_list:
    df = pd.concat([df, df_part])

# Eficiente (acumulando en una lista)
df = pd.concat(df_list)
```

Esto evita la repetición innecesaria de operaciones de concatenación y reduce el uso de memoria.

#### 1.2.4. **Usar `inplace=True` para evitar copias innecesarias**

En operaciones como `drop()`, `fillna()`, y `rename()`, Pandas tiene un parámetro **`inplace`** que permite modificar el DataFrame original sin crear una copia.

```python
# Con inplace=True, no se crea una copia adicional de df
df.drop(columns=['Columna2'], inplace=True)
```

Este tipo de operación es más eficiente en términos de memoria, especialmente cuando trabajas con grandes cantidades de datos.

---

### Resumen

- **Series**: Son unidimensionales, con un índice asociado. Representan una sola columna de datos.
- **DataFrame**: Son bidimensionales y pueden tener múltiples columnas de diferentes tipos de datos.
- **Optimización**: Para trabajar de manera eficiente con grandes conjuntos de datos, utiliza tipos de datos adecuados, evita el uso de `apply()` innecesario y aprovecha funciones como `concat()` y `merge()` para manejar datos de forma más eficiente.
