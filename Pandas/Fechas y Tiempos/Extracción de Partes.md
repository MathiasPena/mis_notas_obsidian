
Pandas proporciona una forma muy útil de extraer componentes específicos de las fechas cuando estas están en un `DatetimeIndex` o una columna con datos de tipo `datetime`. Puedes acceder a varias partes de la fecha, como el año, mes, día, hora, minuto, segundo, etc., utilizando el atributo `.dt`.

### **Sintaxis básica de `.dt`**

Una vez que tienes una columna de fechas en formato `datetime`, puedes acceder a sus componentes usando `.dt`:

```python
import pandas as pd

# Crear un DataFrame con fechas
data = {'fecha': ['2023-01-01', '2023-02-01', '2023-03-01']}
df = pd.DataFrame(data)

# Convertir la columna 'fecha' en tipo datetime
df['fecha'] = pd.to_datetime(df['fecha'])

# Extraer partes de la fecha
df['año'] = df['fecha'].dt.year
df['mes'] = df['fecha'].dt.month
df['día'] = df['fecha'].dt.day

print(df)
```

```
       fecha  año  mes  día
0 2023-01-01  2023    1    1
1 2023-02-01  2023    2    1
2 2023-03-01  2023    3    1
```

### **Extracción de otras partes de la fecha**

Además de año, mes y día, puedes extraer otros componentes importantes de las fechas:

```python
df['hora'] = df['fecha'].dt.hour  # Hora
df['minuto'] = df['fecha'].dt.minute  # Minuto
df['segundo'] = df['fecha'].dt.second  # Segundo
df['nombre_día'] = df['fecha'].dt.day_name()  # Nombre del día de la semana

print(df)
```

```
       fecha  año  mes  día  hora  minuto  segundo nombre_día
0 2023-01-01  2023    1    1     0       0        0     Sunday
1 2023-02-01  2023    2    1     0       0        0   Wednesday
2 2023-03-01  2023    3    1     0       0        0    Wednesday
```

### **Acceder a la parte de fecha de forma más precisa**

Puedes acceder a componentes más específicos de la fecha como el día de la semana, el trimestre o si la fecha pertenece a un año bisiesto:

```python
df['semana'] = df['fecha'].dt.week  # Número de la semana
df['trimestre'] = df['fecha'].dt.quarter  # Trimestre
df['es_bisiesto'] = df['fecha'].dt.is_leap_year  # Año bisiesto

print(df)
```

```
       fecha  año  mes  día  semana  trimestre  es_bisiesto
0 2023-01-01  2023    1    1       1          1        False
1 2023-02-01  2023    2    1       5          1        False
2 2023-03-01  2023    3    1       9          1        False
```

### **Resumen**

- **`.dt`** permite extraer componentes de una columna de fechas.
- Puedes acceder al **año**, **mes**, **día**, **hora**, **minuto**, **segundo**, **nombre del día**, entre otros.
- Funciones como **`day_name()`**, **`week`**, **`quarter`** y **`is_leap_year`** ofrecen detalles adicionales sobre las fechas.

