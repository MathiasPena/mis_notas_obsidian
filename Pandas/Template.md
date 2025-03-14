# Python para Data Engineering - Comandos Básicos

## 1. Manejo de Datos con Pandas

### Cargar datos
```python
import pandas as pd
df = pd.read_csv('archivo.csv')
```

### Ver información básica
```python
df.info()
df.describe()
```

### Seleccionar columnas y filas
```python
df['columna']  # Seleccionar una columna
df.loc[0]      # Seleccionar una fila por índice
df.iloc[0, 1]  # Seleccionar por posición
```

### Filtrado de datos
```python
df[df['columna'] > 10]
df.query('columna == "valor"')
```

### Manejo de valores nulos
```python
df.dropna()
df.fillna(valor)
```

### Agrupación y agregaciones
```python
df.groupby('columna').agg({'otra_columna': 'sum'})
```

---
## 2. Manejo de Archivos

### Leer y escribir archivos CSV
```python
df.to_csv('archivo_salida.csv', index=False)
df = pd.read_csv('archivo.csv', chunksize=1000)  # Lectura eficiente
```

### Leer y escribir en otros formatos
```python
df.to_parquet('archivo.parquet')
df = pd.read_parquet('archivo.parquet')
```

---
## 3. Conexión a Bases de Datos (SQL)

### Conectar con SQLite
```python
import sqlite3
conn = sqlite3.connect('base_de_datos.db')
df = pd.read_sql('SELECT * FROM tabla', conn)
df.to_sql('tabla_nueva', conn, if_exists='replace', index=False)
```

### Conectar con PostgreSQL
```python
from sqlalchemy import create_engine
engine = create_engine('postgresql://usuario:password@host:puerto/basedatos')
df = pd.read_sql('SELECT * FROM tabla', engine)
```

---
## 4. Procesamiento Eficiente

### Uso de `apply()` y vectorización
```python
df['nueva_columna'] = df['columna'].apply(lambda x: x * 2)  # Más lento
df['nueva_columna'] = df['columna'] * 2  # Más rápido
```

### Uso de `numpy` para cálculos eficientes
```python
import numpy as np
df['seno'] = np.sin(df['columna'])
```

---
## 5. Concurrencia y Paralelismo

### Múltiples hilos con `threading`
```python
import threading
def funcion():
    print("Ejecutando en otro hilo")

hilo = threading.Thread(target=funcion)
hilo.start()
hilo.join()
```

### Multiprocesamiento con `multiprocessing`
```python
from multiprocessing import Pool
def cuadrado(x):
    return x * x

with Pool(4) as p:
    print(p.map(cuadrado, [1, 2, 3, 4]))
```

---
## 6. Manejo de Fechas
```python
from datetime import datetime
hoy = datetime.today()
fecha = pd.to_datetime('2024-01-01')
df['fecha'] = pd.to_datetime(df['fecha'])
```

---
## 7. Logging y Debugging
```python
import logging
logging.basicConfig(level=logging.INFO)
logging.info("Esto es un mensaje de log")
```

---
## 8. Buenas Prácticas
- Usar `query()` en vez de filtrado con `[]`.
- Usar `apply()` solo si no hay una alternativa vectorizada.
- Cargar solo las columnas necesarias en `read_csv()`.
- Evitar loops `for` en favor de funciones optimizadas.
