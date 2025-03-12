
En pandas, **combinar datos** es una tarea común cuando trabajas con múltiples DataFrames y deseas unirlos o apilarlos de diferentes maneras. Existen diversas técnicas para combinar datos, como la **concatenación** y el uso de **merge** y **join**, que permiten combinar DataFrames con diferentes estructuras.

---

## 🔹 **Concatenación con `pd.concat()`**

La concatenación es útil cuando quieres apilar **DataFrames** a lo largo de un eje (ya sea filas o columnas). El método `pd.concat()` permite unir **DataFrames** vertical u horizontalmente.

### **Sintaxis básica**

```python
import pandas as pd

# Crear dos DataFrames de ejemplo
df1 = pd.DataFrame({
    'A': [1, 2, 3],
    'B': ['a', 'b', 'c']
})

df2 = pd.DataFrame({
    'A': [4, 5, 6],
    'B': ['d', 'e', 'f']
})

# Concatenar verticalmente (por filas)
df_concat = pd.concat([df1, df2], ignore_index=True)
print(df_concat)
```

```
   A  B
0  1  a
1  2  b
2  3  c
3  4  d
4  5  e
5  6  f
```

### **Concatenación Horizontal**

También puedes concatenar horizontalmente, apilando columnas en lugar de filas. Para esto, se usa el parámetro `axis=1`.

```python
# Concatenar horizontalmente (por columnas)
df_concat = pd.concat([df1, df2], axis=1)
print(df_concat)
```

```
   A  B  A  B
0  1  a  4  d
1  2  b  5  e
2  3  c  6  f
```

### **`ignore_index` y `keys`**

- **`ignore_index=True`**: Restaura los índices, asignando nuevos índices a las filas concatenadas.
- **`keys`**: Permite agregar un nivel de jerarquía al índice resultante.

```python
# Usar 'keys' para agregar un índice jerárquico
df_concat = pd.concat([df1, df2], keys=['DF1', 'DF2'])
print(df_concat)
```

```
        A  B
DF1 0  1  a
    1  2  b
    2  3  c
DF2 0  4  d
    1  5  e
    2  6  f
```

### **Concatenación con diferentes índices**

Si los índices de los DataFrames no coinciden, `pd.concat()` los alineará por índice.

```python
# Crear DataFrames con índices diferentes
df3 = pd.DataFrame({
    'A': [7, 8, 9],
    'B': ['g', 'h', 'i']
}, index=[4, 5, 6])

df_concat = pd.concat([df1, df3], axis=0)
print(df_concat)
```

```
   A  B
0  1  a
1  2  b
2  3  c
4  7  g
5  8  h
6  9  i
```

Si prefieres que los índices se restablezcan automáticamente, puedes usar `ignore_index=True`.

```python
# Restablecer índices
df_concat = pd.concat([df1, df3], axis=0, ignore_index=True)
print(df_concat)
```

```
   A  B
0  1  a
1  2  b
2  3  c
3  7  g
4  8  h
5  9  i
```

### **Concatenación con columnas diferentes**

Si las columnas no coinciden en los DataFrames que estás concatenando, pandas rellenará las columnas faltantes con valores `NaN`.

```python
# Crear DataFrames con columnas diferentes
df4 = pd.DataFrame({
    'A': [10, 11, 12],
    'C': ['j', 'k', 'l']
})

df_concat = pd.concat([df1, df4], axis=0)
print(df_concat)
```

```
     A    B    C
0    1    a  NaN
1    2    b  NaN
2    3    c  NaN
0   10  NaN    j
1   11  NaN    k
2   12  NaN    l
```

---

## 🔹 **Resumen de `pd.concat()`**

- **Concatenación vertical**: `pd.concat([df1, df2])` apila los DataFrames por filas.
- **Concatenación horizontal**: `pd.concat([df1, df2], axis=1)` apila los DataFrames por columnas.
- **`ignore_index=True`**: Restaura los índices, asignando nuevos índices.
- **`keys`**: Crea un índice jerárquico en el resultado.
- **Manejo de diferentes índices**: Los índices no coincidentes se alinean, o puedes restablecerlos con `ignore_index=True`.
- **Diferentes columnas**: Si las columnas no coinciden, se llenan con `NaN`.


