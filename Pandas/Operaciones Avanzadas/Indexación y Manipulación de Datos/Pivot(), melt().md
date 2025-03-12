# Pandas - Indexación y Manipulación de Datos

## **pivot(), melt() para reformatear datos**

En **Pandas**, las funciones **`pivot()`** y **`melt()`** son herramientas poderosas para cambiar la forma de los datos en un **DataFrame**. Son especialmente útiles cuando necesitas reorganizar los datos para facilitar su análisis o visualización.

### **1. pivot()**

La función **`pivot()`** es utilizada para reorganizar los datos, cambiando las columnas de un **DataFrame** en un formato más "ancho". Convierte una columna de valores en varias columnas, basándose en los valores de otras columnas. Esta función es útil cuando tienes datos largos (long format) y los quieres convertir en un formato más compacto o más fácil de analizar.

#### Sintaxis:
```python
DataFrame.pivot(index=None, columns=None, values=None)
```

- **`index`**: El nombre o lista de nombres de las columnas que se convertirán en el índice.
- **`columns`**: El nombre de la columna cuyos valores se convertirán en las columnas del nuevo **DataFrame**.
- **`values`**: El nombre de la columna cuyos valores se distribuirán en las celdas.

#### Ejemplo:
```python
import pandas as pd

# Crear un DataFrame
df = pd.DataFrame({
    'A': ['foo', 'foo', 'bar', 'bar'],
    'B': ['one', 'two', 'one', 'two'],
    'C': [10, 20, 30, 40]
})

# Usar pivot() para reorganizar los datos
pivoted_df = df.pivot(index='A', columns='B', values='C')

print(pivoted_df)
```

Salida:
```
B     one  two
A           
bar   30   40
foo   10   20
```

En este ejemplo, **`pivot()`** convierte la columna **'B'** en las columnas del nuevo **DataFrame**, utilizando los valores de **'C'** para llenar las celdas.

### **2. melt()**

La función **`melt()`** realiza la operación inversa de **`pivot()`**. Transforma un **DataFrame** en un formato más largo, donde las columnas se convierten en filas. Esto es útil cuando se necesitan transformar datos de un formato "ancho" (wide format) a uno "largo" (long format), lo cual es común en visualización de datos o análisis.

#### Sintaxis:
```python
DataFrame.melt(id_vars=None, value_vars=None, var_name=None, value_name='value')
```

- **`id_vars`**: El nombre de las columnas que deben mantenerse como identificadores.
- **`value_vars`**: Las columnas que se deben "derretir" en el formato largo.
- **`var_name`**: El nombre de la nueva columna que representará las variables.
- **`value_name`**: El nombre de la columna que representará los valores.

#### Ejemplo:
```python
import pandas as pd

# Crear un DataFrame
df = pd.DataFrame({
    'A': ['foo', 'bar'],
    'B': [10, 20],
    'C': [30, 40]
})

# Usar melt() para reformatear los datos
melted_df = df.melt(id_vars=['A'], value_vars=['B', 'C'], var_name='Variable', value_name='Value')

print(melted_df)
```

Salida:
```
     A Variable  Value
0  foo        B     10
1  bar        B     20
2  foo        C     30
3  bar        C     40
```

En este ejemplo, **`melt()`** convierte las columnas **'B'** y **'C'** en filas bajo las nuevas columnas **'Variable'** y **'Value'**.

### **3. Comparación entre pivot() y melt()**

- **`pivot()`**: Convierte datos de formato largo a formato ancho, es decir, agrupa valores en columnas.
- **`melt()`**: Convierte datos de formato ancho a formato largo, es decir, deshace el agrupamiento de columnas en filas.

### **4. Conclusión**

- **`pivot()`** es útil cuando se quiere reorganizar los datos para obtener un formato más adecuado para análisis o visualización.
- **`melt()`** es útil para deshacer la organización en columnas y crear un formato largo que se ajusta mejor a ciertos tipos de análisis y visualización de datos.

Ambas funciones son esenciales para manipular y reorganizar datos en **Pandas** de acuerdo a las necesidades del análisis.
