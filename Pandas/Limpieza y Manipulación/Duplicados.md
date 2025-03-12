
Trabajar con datos duplicados es una parte importante de la limpieza de datos. Pandas proporciona varias funciones para identificar, eliminar y manejar duplicados de manera efectiva.

---

## 🔹 Identificación de duplicados: `.duplicated()`

El método `.duplicated()` devuelve un `Series` con valores booleanos (`True` para duplicados y `False` para valores únicos), que puedes usar para filtrar o contar los duplicados en tu DataFrame.

### **Detectar duplicados**:
```python
import pandas as pd

# Crear un DataFrame con duplicados
df = pd.DataFrame({
    "Nombre": ["Ana", "Juan", "Pedro", "Ana", "Juan"],
    "Edad": [25, 30, 22, 25, 30],
})

# Identificar duplicados
print(df.duplicated())
```
```
0    False
1    False
2    False
3     True
4     True
dtype: bool
```

---

## 🔹 Eliminar duplicados: `.drop_duplicates()`

### **Eliminar duplicados en todo el DataFrame**:
```python
# Eliminar duplicados en todo el DataFrame
df_cleaned = df.drop_duplicates()
print(df_cleaned)
```
```
   Nombre  Edad
0    Ana    25
1   Juan    30
2  Pedro    22
```

### **Eliminar duplicados en una columna específica**:
```python
# Eliminar duplicados basados en una sola columna
df_cleaned = df.drop_duplicates(subset="Nombre")
print(df_cleaned)
```
```
   Nombre  Edad
0    Ana    25
1   Juan    30
2  Pedro    22
```

---

## 🔹 Mantener duplicados: `.keep`

Por defecto, `.drop_duplicates()` elimina todos los duplicados, pero puedes usar el argumento `keep` para especificar cuál de los duplicados deseas mantener:

### **Mantener el primer duplicado**:
```python
# Mantener el primer duplicado
df_cleaned = df.drop_duplicates(keep="first")
print(df_cleaned)
```
```
   Nombre  Edad
0    Ana    25
1   Juan    30
2  Pedro    22
```

### **Mantener el último duplicado**:
```python
# Mantener el último duplicado
df_cleaned = df.drop_duplicates(keep="last")
print(df_cleaned)
```
```
   Nombre  Edad
0    Ana    25
1   Juan    30
2  Pedro    22
```

### **Eliminar todos los duplicados**:
```python
# Eliminar todos los duplicados (sin mantener ninguno)
df_cleaned = df.drop_duplicates(keep=False)
print(df_cleaned)
```
```
   Nombre  Edad
2  Pedro    22
```

---

## 🔹 Filtrar y trabajar con duplicados

### **Filtrar filas que no están duplicadas**:
```python
# Filtrar filas que no están duplicadas
df_no_duplicates = df[~df.duplicated()]
print(df_no_duplicates)
```
```
   Nombre  Edad
0    Ana    25
1   Juan    30
2  Pedro    22
```

### **Filtrar solo duplicados**:
```python
# Filtrar solo duplicados
df_duplicates = df[df.duplicated()]
print(df_duplicates)
```
```
   Nombre  Edad
3    Ana    25
4   Juan    30
```

---

## 🔹 Eliminar duplicados en el índice

En ocasiones, los duplicados no solo aparecen en los valores, sino también en los índices. Si tienes duplicados en el índice y quieres eliminarlos:

```python
# Eliminar duplicados en el índice
df = df.set_index('Nombre')
df_cleaned = df[~df.index.duplicated(keep='first')]
print(df_cleaned)
```

---

## 🔹 Combinación con otros métodos

Puedes combinar `.duplicated()` con otros métodos de filtrado o manipulación de datos para una limpieza más avanzada.

### **Filtrar duplicados solo en ciertas columnas**:
```python
# Filtrar duplicados basados en ciertas columnas
df_cleaned = df.drop_duplicates(subset=["Nombre", "Edad"])
print(df_cleaned)
```
```
   Nombre  Edad
0    Ana    25
1   Juan    30
2  Pedro    22
```

### **Filtrar duplicados con condiciones adicionales**:
```python
# Filtrar duplicados con condiciones
df_cleaned = df[df['Edad'] > 25].drop_duplicates(subset='Nombre')
print(df_cleaned)
```
```
   Nombre  Edad
1   Juan    30
2  Pedro    22
```
