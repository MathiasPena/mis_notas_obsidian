
Una **Series** en Pandas es una estructura unidimensional similar a una lista o un array de NumPy, pero con un índice asociado.

---

## 🔹 Crear una `Series`

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

Cada valor tiene un índice automático (0, 1, 2...).

---

## 🔹 Especificar un Índice

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

---

## 🔹 Crear una `Series` desde un Diccionario

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

## 🔹 Acceder a Elementos

```python
print(s["manzanas"])  # 5
print(s[0])  # También se puede acceder por posición
```

📌 También se pueden usar `loc[]` y `iloc[]`:

```python
print(s.loc["naranjas"])  # 3 (por etiqueta)
print(s.iloc[1])  # 3 (por posición)
```

---

## 🔹 Operaciones con `Series`

```python
s2 = pd.Series([2, 3, 4], index=["manzanas", "naranjas", "bananas"])
print(s + s2)  
```
```
manzanas    7
naranjas    6
bananas    11
dtype: int64
```

Si faltan valores, Pandas usa `NaN` (not a number).

---

## 🔹 Métodos Útiles

| Método | Descripción |
|--------|------------|
| `s.sum()` | Suma de valores |
| `s.mean()` | Promedio |
| `s.max()` | Máximo |
| `s.min()` | Mínimo |
| `s.describe()` | Resumen estadístico |
| `s.value_counts()` | Frecuencia de valores |
| `s.apply(función)` | Aplica una función a cada elemento |

Ejemplo:

```python
print(s.sum())  # 15
print(s.apply(lambda x: x * 2))  # Multiplica cada valor por 2
```
