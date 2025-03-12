
En pandas, **agrupación** y **agregación** son procesos esenciales cuando trabajas con grandes volúmenes de datos. Permiten resumir, combinar y realizar estadísticas de grupos de datos similares. El método `.groupby()` es la clave para agrupar, mientras que las funciones de agregación permiten calcular estadísticas sobre esos grupos.

---

## 🔹 `.groupby()`

El método `.groupby()` se usa para dividir un DataFrame en grupos según una o más columnas, para luego aplicar funciones de agregación a esos grupos.

### **Ejemplo básico de `.groupby()`**

Supón que tienes un DataFrame de ventas con las columnas "Producto", "Cantidad" y "Precio":

```python
import pandas as pd

# Crear un DataFrame
df = pd.DataFrame({
    'Producto': ['A', 'B', 'A', 'B', 'A'],
    'Cantidad': [10, 15, 7, 20, 8],
    'Precio': [5, 3, 5, 3, 5]
})

# Agrupar por producto y calcular la suma de las cantidades
df_agrupado = df.groupby('Producto')['Cantidad'].sum()
print(df_agrupado)
```
```
Producto
A    25
B    35
Name: Cantidad, dtype: int64
```

---

## 🔹 Funciones de Agregación

Las funciones de agregación son utilizadas después de agrupar para obtener estadísticas sobre los datos. Algunas de las funciones más comunes son `.sum()`, `.mean()`, `.count()` y `.agg()`.

### **1. `.sum()`**: Suma los valores de cada grupo

```python
# Sumar las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].sum()
print(df_agrupado)
```
```
Producto
A    25
B    35
Name: Cantidad, dtype: int64
```

### **2. `.mean()`**: Calcula el promedio de los valores de cada grupo

```python
# Promedio de precios por producto
df_agrupado = df.groupby('Producto')['Precio'].mean()
print(df_agrupado)
```
```
Producto
A    5.000000
B    3.000000
Name: Precio, dtype: float64
```

### **3. `.count()`**: Cuenta el número de elementos en cada grupo

```python
# Contar la cantidad de registros por producto
df_agrupado = df.groupby('Producto')['Cantidad'].count()
print(df_agrupado)
```
```
Producto
A    3
B    2
Name: Cantidad, dtype: int64
```

### **4. `.agg()`**: Aplica múltiples funciones de agregación a los grupos

El método `.agg()` permite aplicar varias funciones de agregación a una o más columnas.

```python
# Usar .agg() para obtener múltiples agregaciones
df_agrupado = df.groupby('Producto').agg({
    'Cantidad': ['sum', 'mean', 'count'],
    'Precio': 'mean'
})
print(df_agrupado)
```
```
         Cantidad        Precio
             sum mean count   mean
Producto                          
A             25  8.33     3   5.00
B             35 17.50     2   3.00
```

---

## 🔹 Otras Funciones de Agregación

Además de las funciones básicas como `.sum()`, `.mean()`, `.count()` y `.agg()`, existen otras funciones útiles para realizar análisis más detallados:

### **5. `.min()`**: Devuelve el valor mínimo de cada grupo

```python
# Mínimo de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].min()
print(df_agrupado)
```
```
Producto
A    7
B    15
Name: Cantidad, dtype: int64
```

### **6. `.max()`**: Devuelve el valor máximo de cada grupo

```python
# Máximo de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].max()
print(df_agrupado)
```
```
Producto
A    10
B    20
Name: Cantidad, dtype: int64
```

### **7. `.std()`**: Devuelve la desviación estándar de cada grupo

```python
# Desviación estándar de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].std()
print(df_agrupado)
```
```
Producto
A    1.527525
B    3.535534
Name: Cantidad, dtype: float64
```

### **8. `.var()`**: Devuelve la varianza de cada grupo

```python
# Varianza de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].var()
print(df_agrupado)
```
```
Producto
A     2.333333
B    12.500000
Name: Cantidad, dtype: float64
```

### **9. `.median()`**: Devuelve la mediana de cada grupo

```python
# Mediana de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].median()
print(df_agrupado)
```
```
Producto
A     8
B    17
Name: Cantidad, dtype: int64
```

### **10. `.prod()`**: Devuelve el producto de todos los valores en cada grupo

```python
# Producto de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].prod()
print(df_agrupado)
```
```
Producto
A     560
B    300
Name: Cantidad, dtype: int64
```

### **11. `.cumsum()`**: Calcula la suma acumulativa dentro de cada grupo

```python
# Suma acumulativa de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].cumsum()
print(df_agrupado)
```
```
0    10
1    15
2    22
3    42
4    50
Name: Cantidad, dtype: int64
```

### **12. `.cumprod()`**: Calcula el producto acumulativo dentro de cada grupo

```python
# Producto acumulativo de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].cumprod()
print(df_agrupado)
```
```
0      10
1     150
2     105
3    2100
4    16800
Name: Cantidad, dtype: int64
```

### **13. `.first()`**: Devuelve el primer valor de cada grupo

```python
# Primer valor de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].first()
print(df_agrupado)
```
```
Producto
A    10
B    15
Name: Cantidad, dtype: int64
```

### **14. `.last()`**: Devuelve el último valor de cada grupo

```python
# Último valor de las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].last()
print(df_agrupado)
```
```
Producto
A     8
B    20
Name: Cantidad, dtype: int64
```

### **15. `.nunique()`**: Devuelve el número de valores únicos en cada grupo

```python
# Número de valores únicos en las cantidades por producto
df_agrupado = df.groupby('Producto')['Cantidad'].nunique()
print(df_agrupado)
```
```
Producto
A    3
B    2
Name: Cantidad, dtype: int64
```

### **16. `.apply()`**: Permite aplicar cualquier función personalizada a los grupos

```python
# Usar .apply() para aplicar una función personalizada
df_agrupado = df.groupby('Producto').apply(lambda x: x['Cantidad'].sum())
print(df_agrupado)
```
```
Producto
A    25
B    35
dtype: int64
```

### **17. `.describe()`**: Devuelve estadísticas descriptivas como el conteo, media, desviación estándar, etc.

```python
# Obtener estadísticas descriptivas por producto
df_agrupado = df.groupby('Producto').describe()
print(df_agrupado)
```
```
         Cantidad        Precio
             count  mean       count   mean
Producto                                     
A             3.0   8.33         3   5.00
B             2.0  17.50         2   3.00
```

---

## 🔹 Agrupación por Múltiples Columnas

Puedes agrupar por más de una columna. Esto es útil cuando tienes categorías más complejas y deseas calcular estadísticas agrupadas por varias características.

### **Ejemplo: Agrupar por dos columnas**

```python
# Agrupar por 'Producto' y 'Precio' y calcular la suma de las cantidades
df_agrupado = df.groupby(['Producto', 'Precio'])['Cantidad'].sum()
print(df_agrupado)
```
```
Producto  Precio
A         5        25
B         3        35
Name: Cantidad, dtype: int64
```

---

## 🔹 Resumen de `.groupby()` y Funciones de Agregación

- **`.groupby()`**: Divide el DataFrame en grupos según una o más columnas.
- **Funciones de agregación**:
  - `.sum()`, `.mean()`, `.count()`, `.min()`, `.max()`, `.std()`, `.var()`, `.median()`, `.prod()`, `.first()`, `.last()`, `.nunique()`, `.cumsum()`, `.cumprod()`.
  - `.agg()`: Aplica múltiples funciones de agregación a las columnas.
- **Agrupación por múltiples columnas**: Puedes agrupar por más de una columna para obtener estadísticas más complejas.
- **Funciones personalizadas**: Usar `.apply()` para funciones personalizadas a los grupos.
