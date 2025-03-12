

Pandas ofrece varias formas de acceder y seleccionar datos en `Series` y `DataFrames`.

---

## 🔹 Acceder a Datos en una `Series`

### **Por posición** (usando `iloc[]`):
```python
import pandas as pd
s = pd.Series([10, 20, 30, 40], index=["a", "b", "c", "d"])

# Acceder al primer elemento (por posición)
print(s.iloc[0])  # 10
```

### **Por índice** (usando `loc[]`):
```python
# Acceder por índice
print(s.loc["b"])  # 20
```

### **Acceder a un rango de valores**:
```python
# Acceder a un rango (por posición)
print(s.iloc[1:3])  # Desde la posición 1 hasta la 3 (sin incluir la 3)
```

---

## 🔹 Acceder a Datos en un `DataFrame`

### **Por columna**:
```python
# Acceder a una columna
df = pd.DataFrame({
    "Nombre": ["Ana", "Juan", "Pedro"],
    "Edad": [25, 30, 22]
})
print(df["Nombre"])  # Accede a la columna "Nombre"
```

### **Por fila**:
```python
# Acceder a una fila por índice
print(df.loc[1])  # Accede a la fila con índice 1
```

### **Por rango de filas y columnas**:
```python
# Acceder a un rango de filas y columnas
print(df.loc[0:1, "Nombre":"Edad"])  # Filas 0 y 1, columnas desde "Nombre" a "Edad"
```

---

## 🔹 Acceso por `iloc[]` y `loc[]`

### **Acceso por `iloc[]`** (por índice de posición):
```python
# Acceder a una celda (posición)
print(df.iloc[0, 1])  # Fila 0, columna 1 (Ana, 25)
```

### **Acceso por `loc[]`** (por índice de etiqueta):
```python
# Acceder a una celda (por etiqueta)
print(df.loc[0, "Edad"])  # Fila con índice 0, columna "Edad"
```

---

## 🔹 Acceso con `.at[]` y `.iat[]`

### **`.at[]`** (acceso rápido por etiqueta):
```python
# Acceder a una celda usando .at[]
print(df.at[0, "Nombre"])  # "Ana"
```

### **`.iat[]`** (acceso rápido por posición):
```python
# Acceder a una celda usando .iat[]
print(df.iat[0, 0])  # "Ana"
```

---

## 🔹 Filtrar Datos

### **Por condición**:
```python
# Filtrar por condición
print(df[df["Edad"] > 25])  # Filtra las filas donde la edad es mayor a 25
```

### **Por múltiples condiciones**:
```python
# Filtrar con múltiples condiciones
print(df[(df["Edad"] > 25) & (df["Nombre"] == "Juan")])
```
