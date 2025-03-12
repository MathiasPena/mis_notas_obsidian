

En Pandas, el método **`astype()`** es una herramienta clave para optimizar el uso de memoria al convertir los tipos de datos de las columnas de un DataFrame o Series. Al cambiar el tipo de datos de una columna a uno más eficiente, puedes reducir significativamente el tamaño de memoria necesario para almacenar los datos, lo que es especialmente útil cuando trabajas con grandes volúmenes de datos.

### 4.1. ¿Por qué usar `astype()`?

Cuando importamos datos a un DataFrame, Pandas generalmente infiere los tipos de datos. Sin embargo, esta inferencia no siempre es la más eficiente en términos de memoria. Por ejemplo, una columna de enteros que solo contiene valores pequeños podría estar siendo almacenada como **int64**, lo que ocupa más memoria de la necesaria. Usando **`astype()`**, podemos convertir estos tipos de datos a versiones más pequeñas (como **int8** o **float32**) para ahorrar memoria.

#### Ejemplo de uso de **`astype()`** para optimizar memoria:

```python
import pandas as pd
import numpy as np

# Crear un DataFrame con datos de enteros grandes
data = {'col1': [100, 200, 300, 400, 500], 'col2': [1.1, 2.2, 3.3, 4.4, 5.5]}
df = pd.DataFrame(data)

# Ver el tamaño de memoria antes de cambiar el tipo de dato
print("Tamaño antes:", df.memory_usage(deep=True))

# Cambiar el tipo de datos de 'col1' a 'int8' para ahorrar memoria
df['col1'] = df['col1'].astype('int8')

# Ver el tamaño de memoria después de cambiar el tipo de dato
print("Tamaño después:", df.memory_usage(deep=True))
```

Salida:
```
Tamaño antes: 
col1    40
col2    40
dtype: int64
Tamaño después: 
col1    5
col2    40
dtype: int64
```

#### Explicación:
- Inicialmente, **'col1'** tiene un tipo de dato **int64**, lo que hace que ocupe más memoria.
- Al convertir **'col1'** a **int8**, que es un tipo de dato de menor tamaño (ocupa 1 byte en lugar de 8), hemos reducido su tamaño de memoria.

### 4.2. ¿Cuándo usar `astype()`?

- **Reducir el tamaño de memoria**: Si tienes columnas de números enteros o flotantes que no requieren un tipo de dato tan grande, usa **`astype()`** para convertirlos a tipos más pequeños (como **int8**, **int16**, **float32**).
- **Optimización en columnas categóricas**: Si tienes columnas con un número limitado de valores repetidos, como categorías, convertirlas a tipo **Categorical** puede ahorrar mucha memoria.
- **Ajustes después de la carga de datos**: Después de cargar los datos, puedes revisar los tipos de datos de cada columna y realizar conversiones para optimizar el uso de memoria.

### 4.3. Ejemplos de conversiones comunes:

- **`int64` a `int8`, `int16`**: Para reducir el uso de memoria en columnas de enteros con valores pequeños.
- **`float64` a `float32`**: Cuando no necesitas la precisión completa de los flotantes de 64 bits, puedes reducir el tamaño de memoria.
- **`object` a `category`**: Para columnas que contienen un número limitado de valores únicos, usar **Categorical** puede ser una gran optimización.
  
#### Ejemplo de conversión de columna categórica:

```python
df = pd.DataFrame({'Estado': ['Activo', 'Inactivo', 'Activo', 'Pendiente', 'Activo']})

# Convertir la columna 'Estado' a tipo Categorical para reducir la memoria
df['Estado'] = df['Estado'].astype('category')

# Ver el tamaño de memoria de la columna 'Estado'
print(df['Estado'].memory_usage())
```

Salida:
```
64
```

Este tipo de optimización puede ser muy valiosa cuando estás trabajando con grandes volúmenes de datos y quieres reducir el uso de memoria sin perder precisión o información.

### 4.4. Conclusiones:
- **`astype()`** es una forma efectiva de reducir el tamaño de memoria al ajustar los tipos de datos de las columnas.
- Convierte columnas numéricas a tipos de menor tamaño, como **int8**, **float32**, o utiliza **Categorical** para datos con valores limitados y repetidos.
- Esta práctica de optimización es clave para trabajar con grandes conjuntos de datos de manera eficiente.

