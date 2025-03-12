
Un **DataFrame** es una estructura de datos bidimensional (tabla) con filas e índices.

---

## 🔹 Crear un `DataFrame`

Desde un diccionario:

```python
import pandas as pd

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

## 🔹 Especificar un Índice

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

## 🔹 Acceder a Datos

🔸 **Columnas**  
```python
print(df["Nombre"])  # Acceder a una columna
print(df[["Nombre", "Edad"]])  # Acceder a varias
```

🔸 **Filas**  
```python
print(df.loc["a"])  # Acceder por etiqueta
print(df.iloc[0])  # Acceder por posición
```

🔸 **Celda específica**  
```python
print(df.at["a", "Edad"])  # 25
print(df.iat[0, 1])  # 25
```

---

## 🔹 Filtrado de Datos

```python
print(df[df["Edad"] > 25])  # Filtrar por condición
```

---

## 🔹 Operaciones con `DataFrame`

| Método | Descripción |
|--------|------------|
| `df.head(n)` | Primeras `n` filas |
| `df.tail(n)` | Últimas `n` filas |
| `df.info()` | Información general |
| `df.describe()` | Resumen estadístico |
| `df.shape` | Dimensiones del DataFrame |
| `df.columns` | Nombre de columnas |
| `df.index` | Índices |
| `df.sort_values("columna")` | Ordenar por columna |
| `df.fillna(valor)` | Rellenar valores nulos |
| `df.dropna()` | Eliminar filas con `NaN` |
| `df["columna"].apply(func)` | Aplicar función a una columna |

Ejemplo:

```python
df["Edad"] = df["Edad"].apply(lambda x: x + 1)  # Incrementa todas las edades en 1
```
