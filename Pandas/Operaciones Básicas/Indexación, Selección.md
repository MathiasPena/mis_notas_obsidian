
## 🔹 Indexación en Pandas

### **Por columna**:
```python
import pandas as pd
df = pd.DataFrame({
    "Nombre": ["Ana", "Juan", "Pedro"],
    "Edad": [25, 30, 22],
    "Ciudad": ["Madrid", "Barcelona", "Valencia"]
})

# Acceder a una columna (como Series)
print(df["Nombre"])  # Devuelve la columna "Nombre"
```

### **Por fila**:

#### **Acceder a filas por índice (usando `loc[]`)**:
```python
# Acceder a una fila por su índice
print(df.loc[0])  # Fila con índice 0
```

#### **Acceder a filas por posición (usando `iloc[]`)**:
```python
# Acceder a una fila por posición
print(df.iloc[0])  # Fila en la posición 0
```

---

## 🔹 Selección de Datos

### **Selección de una celda**:
```python
# Acceder a una celda por índice (usando .loc[])
print(df.loc[0, "Nombre"])  # Celda en fila 0 y columna "Nombre"
```

```python
# Acceder a una celda por posición (usando .iloc[])
print(df.iloc[0, 0])  # Fila 0, columna 0 (Ana)
```

### **Selección por rango**:

#### **Filas y columnas usando `loc[]`**:
```python
# Selección por rango de filas y columnas (usando .loc[])
print(df.loc[0:1, "Nombre":"Edad"])  # Filas 0 y 1, columnas desde "Nombre" hasta "Edad"
```

#### **Filas y columnas usando `iloc[]`**:
```python
# Selección por rango de filas y columnas (usando .iloc[])
print(df.iloc[0:2, 0:2])  # Filas 0 y 1, columnas 0 y 1
```

---

## 🔹 Filtrado de Datos

### **Por condición**:
```python
# Filtrar por condición
print(df[df["Edad"] > 25])  # Filtra las filas donde la edad es mayor a 25
```

### **Por múltiples condiciones**:
```python
# Filtrar con múltiples condiciones
print(df[(df["Edad"] > 25) & (df["Ciudad"] == "Madrid")])
```

---

## 🔹 Indexación Avanzada

### **Uso de `isin()` para múltiples valores**:
```python
# Filtrar con múltiples valores en una columna
print(df[df["Ciudad"].isin(["Madrid", "Valencia"])])
```

### **Uso de `query()` para expresiones más complejas**:
```python
# Filtrar con expresiones más complejas
print(df.query("Edad > 25 and Ciudad == 'Madrid'"))
```
