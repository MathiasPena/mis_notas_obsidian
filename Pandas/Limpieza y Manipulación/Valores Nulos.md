
El manejo de valores nulos es fundamental para la limpieza de datos. Pandas ofrece varias funciones útiles para tratar estos valores.

---

## 🔹 Identificar valores nulos: `.isna()` y `.isnull()`

Ambos métodos (`isna()` y `isnull()`) funcionan de la misma forma, devuelven un DataFrame/Series con `True` en las posiciones donde hay valores nulos.

```python
import pandas as pd
import numpy as np

# Crear un DataFrame con valores nulos
df = pd.DataFrame({
    "A": [1, 2, np.nan, 4],
    "B": [5, np.nan, 7, 8]
})

# Identificar valores nulos
print(df.isna())
```
```
       A      B
0  False   False
1  False    True
2   True   False
3  False   False
```

---

## 🔹 Filtrar valores nulos

Puedes usar `.isna()` para filtrar filas con valores nulos:

```python
# Filtrar filas que contienen al menos un valor nulo
print(df[df.isna().any(axis=1)])
```

---

## 🔹 Eliminar valores nulos: `.dropna()`

### **Eliminar filas con valores nulos**:
```python
# Eliminar filas con cualquier valor nulo
df_cleaned = df.dropna()
print(df_cleaned)
```
```
     A    B
0  1.0  5.0
3  4.0  8.0
```

### **Eliminar columnas con valores nulos**:
```python
# Eliminar columnas con cualquier valor nulo
df_cleaned = df.dropna(axis=1)
print(df_cleaned)
```
```
     A
0  1.0
1  2.0
3  4.0
```

---

## 🔹 Rellenar valores nulos: `.fillna()`

### **Rellenar con un valor específico**:
```python
# Rellenar los valores nulos con un valor específico
df_filled = df.fillna(0)
print(df_filled)
```
```
     A    B
0  1.0  5.0
1  2.0  0.0
2  0.0  7.0
3  4.0  8.0
```

### **Rellenar con el valor anterior o siguiente**:
```python
# Rellenar los valores nulos con el valor anterior (método de propagación)
df_filled = df.fillna(method="ffill")
print(df_filled)
```
```
     A    B
0  1.0  5.0
1  2.0  5.0
2  2.0  7.0
3  4.0  8.0
```

### **Rellenar con la media, mediana u otros valores**:
```python
# Rellenar valores nulos con la media de la columna
df_filled = df.fillna(df.mean())
print(df_filled)
```
```
     A    B
0  1.0  5.0
1  2.0  6.666667
2  2.333333  7.0
3  4.0  8.0
```

---

## 🔹 Usos Avanzados

### **Rellenar solo en ciertas columnas**:
```python
# Rellenar valores nulos solo en una columna específica
df_filled = df.fillna({"A": 0, "B": 10})
print(df_filled)
```
```
     A    B
0  1.0  5.0
1  2.0  10.0
2  0.0  7.0
3  4.0  8.0
```

---

## 🔹 Métodos Alternativos de Relleno

### **Rellenar con interpolación**:
```python
# Rellenar valores nulos mediante interpolación
df_filled = df.interpolate()
print(df_filled)
```



## **1. `isnull()`**: Detectar Valores Faltantes

La función **`isnull()`** devuelve un DataFrame o Serie booleana donde `True` indica que el valor en esa posición es nulo (faltante), y `False` indica lo contrario.

### Ejemplo: Detectar Valores Nulos

```python
import pandas as pd

# Crear un DataFrame de ejemplo con valores faltantes
data = {'col1': [1, 2, None, 4, 5],
        'col2': ['A', None, 'C', 'D', 'E']}
df = pd.DataFrame(data)

# Detectar valores nulos
print(df.isnull())
```

Esto generará un DataFrame de booleanos que indica si los valores son nulos.

### Argumentos de `isnull()`:
- **`axis`**: Puede especificar el eje sobre el que aplicar la función (0 para filas, 1 para columnas).

## **2. `dropna()`**: Eliminar Valores Faltantes

La función **`dropna()`** permite eliminar filas o columnas con valores faltantes. 

### Ejemplo: Eliminar Filas con Valores Faltantes

```python
# Eliminar filas con valores nulos
df_sin_nulos = df.dropna()

print(df_sin_nulos)
```

Esto eliminará las filas que contienen al menos un valor faltante.

### Argumentos de `dropna()`:
- **`axis`**: Especifica si se eliminarán filas (`axis=0`, por defecto) o columnas (`axis=1`).
- **`how`**: Define el criterio de eliminación. `any` elimina las filas/columnas con al menos un valor nulo, y `all` elimina solo las que tienen todos los valores nulos.
- **`thresh`**: Requiere que una fila o columna tenga al menos un número mínimo de valores no nulos para no ser eliminada.
- **`subset`**: Permite seleccionar un subconjunto de columnas para aplicar la eliminación de valores nulos.

## **3. `fillna()`**: Rellenar Valores Faltantes

La función **`fillna()`** permite rellenar los valores faltantes con un valor específico, una estrategia de interpolación o con el valor de una columna o fila adyacente.

### Ejemplo: Rellenar Valores Faltantes con un Valor Constante

```python
# Rellenar los valores nulos con un valor específico
df_llenado = df.fillna(0)

print(df_llenado)
```

Esto reemplaza los valores nulos en todo el DataFrame con `0`.

### Argumentos de `fillna()`:
- **`value`**: Valor con el que se rellenarán los valores nulos. Puede ser un valor único o un diccionario con valores para columnas específicas.
- **`method`**: Método de relleno. Puede ser `ffill` (relleno hacia adelante) o `bfill` (relleno hacia atrás).
- **`axis`**: El eje sobre el cual rellenar los valores (0 para filas, 1 para columnas).
- **`limit`**: Límite de cuántos valores nulos pueden ser rellenados.

### Ejemplo: Rellenar con el Valor de la Fila Anterior

```python
# Rellenar valores nulos con el valor de la fila anterior (forward fill)
df_llenado_ffill = df.fillna(method='ffill')

print(df_llenado_ffill)
```

Este ejemplo usa el **forward fill** para reemplazar los valores faltantes con los valores previos en la fila.

## **Conclusión**

- **`isnull()`**: Detecta valores faltantes en el DataFrame o Serie.
- **`dropna()`**: Elimina filas o columnas con valores faltantes.
- **`fillna()`**: Rellena los valores faltantes con un valor específico o una estrategia de relleno (como el relleno hacia adelante o hacia atrás).

Estas funciones son esenciales en el preprocesamiento de datos para asegurar que el conjunto de datos esté limpio y listo para su análisis.
