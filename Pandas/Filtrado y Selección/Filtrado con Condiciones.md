
Filtrar datos en pandas es una tarea común y muy poderosa para seleccionar información relevante de un DataFrame. Este proceso se realiza mediante condiciones que permiten aislar los datos que cumplen con ciertos criterios.

---

## 🔹 Filtrar con condiciones simples

Puedes filtrar filas de un DataFrame usando condiciones directamente sobre las columnas. El formato básico es:

```python
df[df['columna'] > valor]
```

### **Ejemplo básico: Filtrar por valores numéricos**
Supongamos que tienes un DataFrame con información de empleados, y deseas filtrar aquellos cuyo salario sea mayor que 50,000:

```python
import pandas as pd

# Crear un DataFrame
df = pd.DataFrame({
    'Empleado': ['Juan', 'Ana', 'Luis', 'Carlos'],
    'Salario': [45000, 55000, 60000, 70000]
})

# Filtrar empleados con salario mayor a 50000
df_filtrado = df[df['Salario'] > 50000]
print(df_filtrado)
```
```
  Empleado  Salario
1     Ana    55000
2    Luis    60000
3  Carlos    70000
```

### **Filtrar con múltiples condiciones (AND, OR)**

Puedes combinar varias condiciones usando los operadores lógicos `&` (AND) y `|` (OR). Ten en cuenta que cada condición debe ir entre paréntesis.

```python
# Filtrar empleados con salario mayor a 50000 y nombre que empieza con 'L'
df_filtrado = df[(df['Salario'] > 50000) & (df['Empleado'].str.startswith('L'))]
print(df_filtrado)
```
```
  Empleado  Salario
2    Luis    60000
```

### **Filtrar con condiciones sobre texto**

Pandas también permite filtrar por condiciones en texto, como verificar si una cadena contiene ciertas palabras.

```python
# Filtrar empleados cuyo nombre contiene 'a'
df_filtrado = df[df['Empleado'].str.contains('a')]
print(df_filtrado)
```
```
  Empleado  Salario
1     Ana    55000
2    Luis    60000
3  Carlos    70000
```

### **Filtrar con rangos de fechas**

Si tu DataFrame tiene columnas de fecha, puedes filtrarlas usando condiciones sobre rangos de fechas.

```python
# Crear un DataFrame con fechas
df = pd.DataFrame({
    'Empleado': ['Juan', 'Ana', 'Luis', 'Carlos'],
    'Ingreso': pd.to_datetime(['2023-01-01', '2024-02-15', '2023-05-20', '2023-07-10'])
})

# Filtrar empleados que ingresaron después de '2023-04-01'
df_filtrado = df[df['Ingreso'] > '2023-04-01']
print(df_filtrado)
```
```
  Empleado      Ingreso
1     Ana    2024-02-15
2    Luis    2023-05-20
3  Carlos    2023-07-10
```

---

## 🔹 Filtrar con condiciones más complejas

Puedes aplicar múltiples condiciones complejas en las que puedes usar funciones para transformar los datos antes de filtrarlos.

### **Ejemplo: Filtrar con una condición personalizada**
Si quisieras filtrar empleados cuyo salario sea mayor al promedio, puedes hacerlo con una función que calcule ese valor:

```python
# Calcular salario promedio
salario_promedio = df['Salario'].mean()

# Filtrar empleados cuyo salario es mayor al promedio
df_filtrado = df[df['Salario'] > salario_promedio]
print(df_filtrado)
```
```
  Empleado  Salario
2    Luis    60000
3  Carlos    70000
```

---

## 🔹 Resumen de Filtrado con Condiciones

- **Operadores lógicos**: Usa `&` para "AND" y `|` para "OR" en condiciones múltiples.
- **Filtrado por texto**: Usa `.str.contains()`, `.str.startswith()`, `.str.endswith()` para trabajar con cadenas.
- **Fechas**: Puedes filtrar basándote en rangos de fechas si tienes una columna de tipo `datetime`.
- **Condiciones personalizadas**: Usa funciones como `.apply()` para crear filtros más avanzados y personalizados.

