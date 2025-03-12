
A diferencia de la concatenación, que apila los DataFrames, **`merge`** y **`join`** son métodos utilizados para combinar DataFrames basándose en columnas o índices comunes, similar a lo que se hace en bases de datos con las operaciones de **JOIN**.

### **`pd.merge()`**

`pd.merge()` es una de las formas más flexibles y poderosas de combinar DataFrames. Permite combinar dos DataFrames basándose en una o más columnas clave, y se puede controlar cómo se combinan los datos.

#### **Sintaxis básica**

```python
import pandas as pd

# DataFrames de ejemplo
df1 = pd.DataFrame({
    'ID': [1, 2, 3, 4],
    'Nombre': ['Ana', 'Luis', 'Pedro', 'Marta'],
    'Edad': [23, 35, 45, 36]
})

df2 = pd.DataFrame({
    'ID': [2, 3, 4, 5],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})

# Combinar por columna 'ID'
df_merged = pd.merge(df1, df2, on='ID')
print(df_merged)
```

```
   ID  Nombre  Edad    Ciudad
0   2    Luis    35    Madrid
1   3   Pedro    45  Barcelona
2   4   Marta    36   Valencia
```

### **Tipos de Merge**

Puedes especificar qué tipo de "join" quieres realizar con el parámetro `how`. Los tipos más comunes son:

- **`how='inner'`**: Solo devuelve las filas con claves comunes en ambos DataFrames. Este es el valor por defecto.
- **`how='left'`**: Mantiene todas las filas del DataFrame de la izquierda y solo las coincidencias del DataFrame de la derecha.
- **`how='right'`**: Mantiene todas las filas del DataFrame de la derecha y solo las coincidencias del DataFrame de la izquierda.
- **`how='outer'`**: Devuelve todas las filas de ambos DataFrames y rellena con `NaN` donde no haya coincidencia.

```python
# Merge con diferentes tipos de join
df_left = pd.merge(df1, df2, on='ID', how='left')
df_right = pd.merge(df1, df2, on='ID', how='right')
df_outer = pd.merge(df1, df2, on='ID', how='outer')

print(df_left)
print(df_right)
print(df_outer)
```

#### **Resultados**:

**`how='left'`** (mantiene todas las filas del DataFrame izquierdo):

```
   ID  Nombre  Edad    Ciudad
0   1     Ana    23      NaN
1   2    Luis    35    Madrid
2   3   Pedro    45  Barcelona
3   4   Marta    36   Valencia
```

**`how='right'`** (mantiene todas las filas del DataFrame derecho):

```
   ID  Nombre  Edad    Ciudad
0   2    Luis    35    Madrid
1   3   Pedro    45  Barcelona
2   4   Marta    36   Valencia
3   5     NaN   NaN    Sevilla
```

**`how='outer'`** (mantiene todas las filas de ambos):

```
   ID  Nombre  Edad    Ciudad
0   1     Ana    23      NaN
1   2    Luis    35    Madrid
2   3   Pedro    45  Barcelona
3   4   Marta    36   Valencia
4   5     NaN   NaN    Sevilla
```

### **Merge por múltiples columnas**

Si tienes varias columnas clave por las cuales hacer el merge, puedes usar una lista de nombres de columnas en el parámetro `on`.

```python
df1 = pd.DataFrame({
    'ID': [1, 2, 3, 4],
    'Edad': [23, 35, 45, 36],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Madrid']
})

df2 = pd.DataFrame({
    'ID': [2, 3, 4, 5],
    'Edad': [35, 45, 36, 50],
    'Nombre': ['Luis', 'Pedro', 'Marta', 'Carlos']
})

df_merged = pd.merge(df1, df2, on=['ID', 'Edad'])
print(df_merged)
```

```
   ID  Edad    Ciudad  Nombre
0   2    35  Barcelona    Luis
1   3    45  Barcelona   Pedro
2   4    36   Valencia   Marta
```

### **`df.join()`**

El método `.join()` es una forma más sencilla de realizar un merge, pero tiene algunas limitaciones, como que solo permite realizar un join con el índice (en lugar de una o más columnas específicas). Sin embargo, es útil cuando estás trabajando con índices como claves para la combinación.

#### **Sintaxis básica**

```python
df1 = pd.DataFrame({
    'ID': [1, 2, 3],
    'Nombre': ['Ana', 'Luis', 'Pedro']
})
df2 = pd.DataFrame({
    'ID': [1, 2, 3],
    'Edad': [23, 35, 45]
}).set_index('ID')

df_joined = df1.join(df2, on='ID')
print(df_joined)
```

```
   ID  Nombre  Edad
0   1     Ana    23
1   2    Luis    35
2   3   Pedro    45
```

### **`join()` con índices diferentes**

Si los DataFrames tienen diferentes índices, puedes especificar el índice en el parámetro `on` y realizar el join. También puedes controlar el tipo de join con `how`.

```python
df1 = pd.DataFrame({
    'ID': [1, 2, 3],
    'Nombre': ['Ana', 'Luis', 'Pedro']
})
df2 = pd.DataFrame({
    'Edad': [23, 35, 45]
}, index=[1, 2, 3])

df_joined = df1.set_index('ID').join(df2, how='inner')
print(df_joined)
```

```
   Nombre  Edad
ID              
1     Ana    23
2    Luis    35
3   Pedro    45
```

---

## 🔹 **Resumen de `pd.merge()` y `.join()`**

- **`pd.merge()`**: Método flexible que permite combinar DataFrames basándose en una o más columnas clave. Soporta diferentes tipos de joins: `inner`, `left`, `right`, `outer`.
- **`df.join()`**: Utiliza los índices de los DataFrames para realizar el join. Es más sencillo de usar, pero menos flexible que `merge()`.
- **Merge por múltiples columnas**: Puedes realizar un merge utilizando varias columnas clave.
- **Flexibilidad**: Ambos métodos permiten controlar cómo se combinan los datos y manejar los valores no coincidentes.

