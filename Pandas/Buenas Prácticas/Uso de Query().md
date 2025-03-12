# Buenas Prácticas en Pandas: Uso de `query()` para Filtros Eficientes

La función **`query()`** en Pandas es una herramienta poderosa y eficiente para filtrar datos en un DataFrame. Utilizar **`query()`** mejora la legibilidad del código y, en muchos casos, ofrece un mejor rendimiento en comparación con la indexación tradicional.

## **1. ¿Qué es `query()`?**

La función **`query()`** permite realizar filtros en un DataFrame utilizando una cadena de texto que especifica la condición. Esta forma de filtrar datos es más concisa y legible, especialmente cuando las condiciones son complejas.

## **2. Uso Básico de `query()`**

### Ejemplo: Filtro Simple

```python
import pandas as pd

# Crear un DataFrame de ejemplo
data = {'col1': [10, 20, 30, 40, 50],
        'col2': ['a', 'b', 'c', 'd', 'e']}
df = pd.DataFrame(data)

# Usar query() para filtrar donde col1 sea mayor a 20
df_filtrado = df.query('col1 > 20')

print(df_filtrado)
```

En este caso, **`query()`** selecciona todas las filas donde el valor de `col1` es mayor que 20.

## **3. Filtrar con Condiciones Compuestas**

También puedes usar operadores lógicos como **`and`**, **`or`** y **`not`** para combinar múltiples condiciones.

### Ejemplo: Condiciones Compuestas

```python
# Filtrar con múltiples condiciones
df_filtrado_multiple = df.query('col1 > 20 and col2 == "c"')

print(df_filtrado_multiple)
```

Este filtro selecciona las filas donde **`col1 > 20`** y **`col2 == "c"`**.

## **4. Uso de Variables en `query()`**

**`query()`** permite el uso de variables dentro de la cadena de consulta, lo que permite crear consultas más dinámicas.

```python
# Filtrar usando variables externas
umbral = 30
df_filtrado_variable = df.query('col1 > @umbral')

print(df_filtrado_variable)
```

El símbolo **`@`** permite acceder a variables externas dentro del contexto de la consulta.

## **5. Ventajas de Usar `query()`**

- **Mejor legibilidad**: La sintaxis es más concisa y fácil de entender que las versiones tradicionales de filtrado como `df[df['col1'] > 20]`.
- **Optimización**: En ciertos casos, **`query()`** puede ser más rápido, especialmente cuando se trabaja con DataFrames grandes, ya que internamente utiliza **`numexpr`** para evaluar las expresiones.
- **Expresiones complejas**: Permite realizar filtros con múltiples condiciones de manera muy limpia y organizada.

## **6. Consideraciones y Limitaciones**

- **Variables en el entorno**: Cuando uses **`query()`** con variables, asegúrate de que las variables estén definidas en el entorno global, de lo contrario, Pandas no podrá acceder a ellas.
- **Tipos de datos**: **`query()`** es más eficiente para trabajar con columnas numéricas y cadenas de texto. Si usas tipos de datos complejos o personalizados, ten en cuenta que **`query()`** puede no ser tan eficiente o incluso fallar.
- **Compatibilidad**: Aunque **`query()`** es muy eficiente, no todas las operaciones que puedes hacer con indexación tradicional se pueden realizar con **`query()`**.

## **7. Conclusión**

Usar **`query()`** para realizar filtros en Pandas es una excelente práctica para mejorar la legibilidad, simplificar el código y, en algunos casos, mejorar el rendimiento. Su sintaxis permite trabajar con expresiones lógicas complejas de manera más clara, y su integración con variables externas lo hace aún más versátil.
