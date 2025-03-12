
### **`sort_values()`**

El método **`sort_values()`** se utiliza para ordenar un DataFrame o Series según los valores de una o más columnas. Puedes especificar el orden (ascendente o descendente) con el parámetro `ascending`.

#### **Sintaxis básica**

```python
import pandas as pd

df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Pedro', 'Marta'],
    'Edad': [23, 35, 45, 36]
})

# Ordenar por la columna 'Edad' de menor a mayor
df_sorted = df.sort_values(by='Edad')
print(df_sorted)
```

```
   Nombre  Edad
0     Ana    23
1    Luis    35
3   Marta    36
2   Pedro    45
```

#### **Ordenación descendente**

```python
# Ordenar por 'Edad' de mayor a menor
df_sorted_desc = df.sort_values(by='Edad', ascending=False)
print(df_sorted_desc)
```

```
   Nombre  Edad
2   Pedro    45
3   Marta    36
1    Luis    35
0     Ana    23
```

#### **Ordenar por múltiples columnas**

Puedes ordenar por varias columnas pasando una lista de nombres de columnas al parámetro `by`. 

```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Pedro', 'Marta'],
    'Edad': [23, 35, 45, 36],
    'Salario': [1500, 2500, 2200, 1800]
})

# Ordenar por 'Edad' y luego por 'Salario'
df_sorted_multi = df.sort_values(by=['Edad', 'Salario'], ascending=[True, False])
print(df_sorted_multi)
```

```
   Nombre  Edad  Salario
0     Ana    23     1500
1    Luis    35     2500
3   Marta    36     1800
2   Pedro    45     2200
```

---

### **`sort_index()`**

El método **`sort_index()`** permite ordenar los DataFrames y Series por sus índices. Este método es útil cuando necesitas organizar los datos según el índice.

#### **Sintaxis básica**

```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Pedro', 'Marta'],
    'Edad': [23, 35, 45, 36]
}, index=[3, 1, 4, 2])

# Ordenar por índice de menor a mayor
df_sorted_index = df.sort_index()
print(df_sorted_index)
```

```
   Nombre  Edad
1    Luis    35
2   Marta    36
3     Ana    23
4   Pedro    45
```

#### **Ordenación descendente por índice**

```python
# Ordenar por índice de mayor a menor
df_sorted_index_desc = df.sort_index(ascending=False)
print(df_sorted_index_desc)
```

```
   Nombre  Edad
4   Pedro    45
3     Ana    23
2   Marta    36
1    Luis    35
```

---

### **`rank()`**

El método **`rank()`** se usa para asignar un ranking a los elementos en una columna o fila, basándose en sus valores. Es útil cuando necesitas encontrar la posición relativa de los datos en términos de su magnitud.

#### **Sintaxis básica**

```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Pedro', 'Marta'],
    'Edad': [23, 35, 45, 36]
})

# Obtener el ranking de la columna 'Edad'
df['Ranking'] = df['Edad'].rank()
print(df)
```

```
   Nombre  Edad  Ranking
0     Ana    23      1.0
1    Luis    35      2.0
3   Marta    36      3.0
2   Pedro    45      4.0
```

#### **Ranking con valores duplicados**

Cuando hay valores duplicados, el ranking asigna el promedio de los rangos a esos valores.

```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Pedro', 'Marta'],
    'Edad': [23, 35, 35, 36]
})

# Obtener el ranking de la columna 'Edad' con valores duplicados
df['Ranking'] = df['Edad'].rank()
print(df)
```

```
   Nombre  Edad  Ranking
0     Ana    23      1.0
1    Luis    35      2.5
2   Pedro    35      2.5
3   Marta    36      4.0
```

#### **Ranking descendente**

Para ordenar el ranking de manera descendente, puedes usar el parámetro `ascending=False`.

```python
df['Ranking_desc'] = df['Edad'].rank(ascending=False)
print(df)
```

```
   Nombre  Edad  Ranking  Ranking_desc
0     Ana    23      1.0           4.0
1    Luis    35      2.5           3.0
2   Pedro    35      2.5           3.0
3   Marta    36      4.0           1.0
```

---

## 🔹 **Resumen de métodos de Ordenamiento y Ranking**

- **`sort_values()`**: Ordena un DataFrame o Series por los valores de una o más columnas, con opciones de orden ascendente o descendente.
- **`sort_index()`**: Ordena el DataFrame o Series por el índice.
- **`rank()`**: Asigna un ranking a los elementos de una columna o fila, con opciones de manejar valores duplicados y ordenar de forma ascendente o descendente.

