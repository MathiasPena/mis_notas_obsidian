
Pandas ofrece una forma más elegante y flexible de filtrar datos usando el método `.query()`. Este método permite utilizar expresiones en formato de cadena para filtrar el DataFrame, lo que facilita la legibilidad y escritura del código, especialmente cuando se tienen condiciones complejas.

---

## 🔹 Uso Básico de `.query()`

El método `.query()` permite aplicar una condición como una cadena dentro de la cual puedes usar los nombres de las columnas directamente, sin necesidad de referirlas con `df['columna']`.

### **Ejemplo básico de `.query()`**

Supongamos que tienes un DataFrame con datos de productos y quieres filtrar aquellos con un precio mayor a 100:

```python
import pandas as pd

# Crear un DataFrame
df = pd.DataFrame({
    'Producto': ['A', 'B', 'C', 'D'],
    'Precio': [50, 150, 200, 80]
})

# Filtrar productos con precio mayor a 100 usando .query()
df_filtrado = df.query('Precio > 100')
print(df_filtrado)
```
```
  Producto  Precio
1        B     150
2        C     200
```

---

## 🔹 Uso de Condiciones Combinadas en `.query()`

Puedes combinar múltiples condiciones usando operadores lógicos como `and`, `or`, y `not`. Recuerda que en `.query()`, debes usar `and` en lugar de `&` y `or` en lugar de `|`.

### **Ejemplo: Filtrar con condiciones múltiples**

Si quieres filtrar productos cuyo precio sea mayor a 100 y el nombre del producto sea 'B' o 'C':

```python
df_filtrado = df.query('Precio > 100 and (Producto == "B" or Producto == "C")')
print(df_filtrado)
```
```
  Producto  Precio
1        B     150
2        C     200
```

---

## 🔹 Filtrado con Cadenas de Texto

Si tienes columnas de texto, puedes utilizar las mismas funciones que en el filtrado normal, pero con la sintaxis de `.query()`:

### **Ejemplo: Filtrar por cadenas que contienen una letra**

Supón que tienes una columna de texto con nombres de personas y quieres filtrar aquellos que contienen la letra "a":

```python
df = pd.DataFrame({
    'Nombre': ['Juan', 'Ana', 'Luis', 'Carlos'],
    'Edad': [30, 25, 40, 35]
})

# Filtrar nombres que contienen la letra 'a'
df_filtrado = df.query('Nombre.str.contains("a")', engine='python')
print(df_filtrado)
```
```
  Nombre  Edad
0   Juan    30
1    Ana    25
3 Carlos    35
```

---

## 🔹 Filtrado con Variables Externas

También puedes usar variables externas en las condiciones dentro de `.query()` al pasarlas como parámetros con el prefijo `@`.

### **Ejemplo: Usar una variable externa**

Si tienes una variable externa y quieres usarla en el filtrado:

```python
umbral_precio = 100

# Filtrar productos cuyo precio sea mayor al valor de 'umbral_precio'
df_filtrado = df.query('Precio > @umbral_precio')
print(df_filtrado)
```
```
  Producto  Precio
1        B     150
2        C     200
```

---

## 🔹 Comparación entre `.query()` y el Filtrado Tradicional

- **Ventajas de `.query()`**: Más legible, sobre todo con condiciones complejas. Puede ser más conveniente al trabajar con muchas condiciones.
- **Limitaciones**: No puedes usar el nombre de las columnas que contienen espacios u otros caracteres especiales. Necesitas usar el motor de Python (`engine='python'`) si trabajas con funciones de cadena como `.str.contains()`, ya que por defecto `.query()` usa el motor de expresiones de pandas.

---

## 🔹 Resumen de `.query()`

- **Sintaxis clara**: Usa expresiones de tipo cadena para filtrar datos.
- **Operadores lógicos**: Usa `and`, `or`, `not` en lugar de `&` y `|`.
- **Funcionalidad con texto**: Puedes filtrar cadenas usando `.query()`, aunque algunas funciones de cadenas requieren el motor `python`.
- **Variables externas**: Usa variables externas con el prefijo `@` dentro de la condición.
