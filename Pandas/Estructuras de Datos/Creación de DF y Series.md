
## 🔹 Crear una `Series`

Una `Series` es una estructura unidimensional con datos etiquetados (índices).

```python
import pandas as pd

# Desde una lista
s = pd.Series([10, 20, 30, 40])
print(s)
```
```
0    10
1    20
2    30
3    40
dtype: int64
```

**Con índice personalizado**:
```python
s = pd.Series([10, 20, 30], index=["a", "b", "c"])
print(s)
```
```
a    10
b    20
c    30
dtype: int64
```

**Desde un diccionario**:
```python
datos = {"manzanas": 5, "naranjas": 3, "bananas": 7}
s = pd.Series(datos)
print(s)
```
```
manzanas    5
naranjas    3
bananas     7
dtype: int64
```

---

## 🔹 Crear un `DataFrame`

Un `DataFrame` es una estructura bidimensional (tabla) con filas y columnas.

**Desde un diccionario de listas**:
```python
datos = {
    "Nombre": ["Ana", "Juan", "Pedro"],
    "Edad": [25, 30, 22],
    "Ciudad": ["Madrid", "Barcelona", "Valencia"]
}
df = pd.DataFrame(datos)
print(df)
```
```
  Nombre  Edad    Ciudad
0    Ana    25    Madrid
1   Juan    30  Barcelona
2  Pedro    22  Valencia
```

---

## 🔹 Crear un `DataFrame` desde un Archivo CSV

```python
# Cargar un CSV en un DataFrame
df = pd.read_csv("archivo.csv")
print(df)
```

---

## 🔹 Crear un `DataFrame` con Índice Personalizado

```python
df = pd.DataFrame(datos, index=["a", "b", "c"])
print(df)
```
```
  Nombre  Edad    Ciudad
a    Ana    25    Madrid
b   Juan    30  Barcelona
c  Pedro    22  Valencia
```

---

## 🔹 Crear un `DataFrame` desde un Archivo Excel

```python
df = pd.read_excel("archivo.xlsx")
print(df)
```

---

Estas son las formas más comunes de crear **Series** y **DataFrames** en Pandas. 🚀
