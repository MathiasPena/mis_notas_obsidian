
Pandas ofrece varias funciones para transformar datos de manera eficiente. Las transformaciones pueden incluir aplicar funciones a columnas o filas, realizar mapeo de valores o reemplazos, y aplicar funciones personalizadas.

---

## 🔹 Aplicar funciones: `.apply()`

El método `.apply()` te permite aplicar una función a lo largo de un eje (filas o columnas) de un DataFrame o Series.

### **Aplicar una función a una columna (Series)**:
```python
import pandas as pd

# Crear un DataFrame
df = pd.DataFrame({
    "Edad": [25, 30, 35, 40],
    "Salario": [50000, 60000, 70000, 80000]
})

# Aplicar una función que incrementa cada valor de la columna
df["Edad_incremetada"] = df["Edad"].apply(lambda x: x + 1)
print(df)
```
```
   Edad  Salario  Edad_incremetada
0    25    50000                26
1    30    60000                31
2    35    70000                36
3    40    80000                41
```

### **Aplicar una función a todo el DataFrame**:
```python
# Aplicar una función a cada columna
df_transformed = df.apply(lambda x: x * 2)
print(df_transformed)
```
```
   Edad  Salario  Edad_incremetada
0    50   100000                52
1    60   120000                62
2    70   140000                72
3    80   160000                82
```

---

## 🔹 Mapeo de valores: `.map()`

El método `.map()` es útil cuando necesitas transformar o mapear valores individuales de una Series según un diccionario o función.

### **Mapear valores con un diccionario**:
```python
# Crear un DataFrame
df = pd.DataFrame({
    "Estado": ["Aprobado", "Reprobado", "Aprobado", "Aprobado"]
})

# Mapear los valores usando un diccionario
estado_map = {"Aprobado": 1, "Reprobado": 0}
df["Estado_numerico"] = df["Estado"].map(estado_map)
print(df)
```
```
     Estado  Estado_numerico
0  Aprobado               1
1  Reprobado               0
2  Aprobado               1
3  Aprobado               1
```

### **Mapear valores con una función**:
```python
# Usar una función para transformar
df["Estado_upper"] = df["Estado"].map(lambda x: x.upper())
print(df)
```
```
     Estado  Estado_numerico Estado_upper
0  Aprobado               1      APROBADO
1  Reprobado               0    REPROBADO
2  Aprobado               1      APROBADO
3  Aprobado               1      APROBADO
```

---

## 🔹 Reemplazar valores: `.replace()`

El método `.replace()` permite reemplazar valores específicos de una Series o DataFrame con otros valores.

### **Reemplazar valores en una columna**:
```python
# Crear un DataFrame
df = pd.DataFrame({
    "Estado": ["Aprobado", "Reprobado", "Aprobado", "Aprobado"]
})

# Reemplazar valores
df["Estado"] = df["Estado"].replace("Aprobado", "Pasado")
print(df)
```
```
    Estado
0   Pasado
1  Reprobado
2   Pasado
3   Pasado
```

### **Reemplazar varios valores a la vez**:
```python
# Reemplazar múltiples valores a la vez
df["Estado"] = df["Estado"].replace({"Pasado": "Aprobado", "Reprobado": "Fallido"})
print(df)
```
```
     Estado
0  Aprobado
1   Fallido
2  Aprobado
3  Aprobado
```

---

## 🔹 Transformaciones avanzadas: `.applymap()`

El método `.applymap()` se usa para aplicar una función a todos los elementos de un DataFrame. A diferencia de `.apply()`, que se usa en columnas o filas, `.applymap()` trabaja sobre cada valor del DataFrame.

### **Aplicar una función a todos los elementos**:
```python
# Crear un DataFrame
df = pd.DataFrame({
    "Edad": [25, 30, 35, 40],
    "Salario": [50000, 60000, 70000, 80000]
})

# Aplicar una función a todos los valores
df_transformed = df.applymap(lambda x: x * 1.1)
print(df_transformed)
```
```
    Edad   Salario
0   27.5   55000.0
1   33.0   66000.0
2   38.5   77000.0
3   44.0   88000.0
```

---

## 🔹 Combinación con otros métodos

Puedes combinar `.apply()`, `.map()` y `.replace()` con otros métodos de pandas para realizar transformaciones complejas y personalizadas.

### **Transformar con condiciones**:
```python
# Aplicar una función con una condición
df["Salario_incrementado"] = df["Salario"].apply(lambda x: x * 1.05 if x > 60000 else x)
print(df)
```
```
   Edad  Salario  Salario_incrementado
0    25    50000                50000.0
1    30    60000                60000.0
2    35    70000                73500.0
3    40    80000                84000.0
```

---

## 🔹 Resumen de los métodos

- `.apply()`: Aplica una función a lo largo de filas o columnas de un DataFrame o Series.
- `.map()`: Aplica una función o un mapeo (diccionario) a cada elemento de una Series.
- `.replace()`: Reemplaza valores específicos dentro de una Series o DataFrame.
- `.applymap()`: Aplica una función a cada valor de un DataFrame completo.
