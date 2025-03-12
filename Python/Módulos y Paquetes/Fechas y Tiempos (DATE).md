
Python tiene el módulo `datetime` para trabajar con fechas y tiempos. También incluye `timedelta` para operaciones con fechas.

---

## 🔹 `datetime`: Fecha y Hora Actual

```python
from datetime import datetime

ahora = datetime.now()
print(ahora)  # Ej: 2025-03-10 14:30:15.123456

print(ahora.year)   # Año
print(ahora.month)  # Mes
print(ahora.day)    # Día
print(ahora.hour)   # Hora
print(ahora.minute) # Minuto
print(ahora.second) # Segundo
```

---

## 🔹 Crear Fechas Personalizadas

```python
from datetime import datetime

fecha = datetime(2025, 12, 31, 23, 59, 59)
print(fecha)  # 2025-12-31 23:59:59
```

---

## 🔹 `timedelta`: Operaciones con Fechas

```python
from datetime import datetime, timedelta

hoy = datetime.now()
mañana = hoy + timedelta(days=1)
ayer = hoy - timedelta(days=1)

print(mañana)  # Fecha de mañana
print(ayer)    # Fecha de ayer

# Diferencia entre fechas
diferencia = mañana - ayer
print(diferencia.days)  # 2 días
```

---

## 🔹 Formateo de Fechas (`strftime`)

```python
from datetime import datetime

fecha = datetime(2025, 3, 10, 14, 30)
print(fecha.strftime("%d/%m/%Y"))  # 10/03/2025
print(fecha.strftime("%H:%M:%S"))  # 14:30:00
print(fecha.strftime("%A"))  # Lunes (día de la semana)
```

📌 **Formato común:**
- `%Y` → Año completo (2025)
- `%y` → Año corto (25)
- `%m` → Mes (03)
- `%d` → Día (10)
- `%H` → Hora (24h)
- `%I` → Hora (12h)
- `%M` → Minuto
- `%S` → Segundo
- `%A` → Día de la semana

---

## 🔹 Convertir String a Fecha (`strptime`)

```python
from datetime import datetime

fecha_str = "10/03/2025 14:30"
fecha_obj = datetime.strptime(fecha_str, "%d/%m/%Y %H:%M")

print(fecha_obj)  # 2025-03-10 14:30:00
```

---

## 🔥 Resumen

| Función | Descripción |
|---------|------------|
| `datetime.now()` | Obtiene la fecha y hora actual |
| `datetime(año, mes, día, hora, min, seg)` | Crea una fecha específica |
| `timedelta(days=n)` | Operaciones con fechas |
| `strftime(formato)` | Formatea fechas en texto |
| `strptime(texto, formato)` | Convierte texto en fecha |



El módulo `datetime` de Python proporciona clases para manipular fechas y horas de manera sencilla y eficiente. En el contexto de **Data Engineering**, manejar correctamente las fechas es crucial, ya que muchos procesos involucran timestamps, intervalos de tiempo y comparaciones de fechas.

---

## 🔹 ¿Qué es `datetime`?

El módulo `datetime` proporciona varias clases para trabajar con fechas y horas, entre ellas:

- **`datetime.date`**: Para trabajar con fechas (año, mes, día).
- **`datetime.time`**: Para trabajar con tiempos (hora, minuto, segundo, microsegundo).
- **`datetime.datetime`**: Combinación de fecha y hora.
- **`datetime.timedelta`**: Para representar la diferencia entre dos fechas o tiempos.
- **`datetime.tzinfo`**: Para manejar zonas horarias.

---

## 🔹 Crear Fechas y Tiempos con `datetime`

### 🛠️ Ejemplo: Crear un objeto `datetime`

```python
from datetime import datetime

# Crear un objeto datetime con fecha y hora actual
ahora = datetime.now()
print(ahora)  # Ejemplo de salida: 2025-03-11 14:30:59.123456

# Crear un objeto datetime con una fecha y hora específica
fecha_especifica = datetime(2025, 3, 11, 14, 30, 59)
print(fecha_especifica)  # 2025-03-11 14:30:59
```

📌 **Explicación:**
- `datetime.now()` devuelve la fecha y hora actual.
- Puedes crear una instancia de `datetime` proporcionando el año, mes, día, hora, minuto, segundo, y microsegundo.

---

## 🔹 Formato de Fechas y Tiempos (`strftime` y `strptime`)

### 🛠️ Ejemplo: Formatear Fechas con `strftime`

```python
# Formatear la fecha actual en un formato específico
fecha_formateada = ahora.strftime("%Y-%m-%d %H:%M:%S")
print(fecha_formateada)  # Ejemplo: 2025-03-11 14:30:59
```

📌 **Explicación:**
- `strftime` convierte un objeto `datetime` en un string según el formato especificado.
- Los códigos comunes son:
  - `%Y`: Año con 4 dígitos
  - `%m`: Mes
  - `%d`: Día
  - `%H`: Hora (24 horas)
  - `%M`: Minuto
  - `%S`: Segundo

### 🛠️ Ejemplo: Parsear Cadenas a Fechas con `strptime`

```python
# Convertir una cadena a un objeto datetime
fecha_parseada = datetime.strptime("2025-03-11 14:30:59", "%Y-%m-%d %H:%M:%S")
print(fecha_parseada)  # 2025-03-11 14:30:59
```

📌 **Explicación:**
- `strptime` convierte una cadena en un objeto `datetime` según el formato proporcionado.

---

## 🔹 Operaciones con Fechas: `timedelta`

`timedelta` se usa para realizar operaciones aritméticas con fechas, como sumar o restar días, horas, minutos, etc.

### 🛠️ Ejemplo: Operaciones con `timedelta`

```python
from datetime import timedelta

# Crear un objeto timedelta
diferencia = timedelta(days=5, hours=3)

# Sumar o restar un timedelta a una fecha
nueva_fecha = ahora + diferencia
print(nueva_fecha)  # Fecha actual más 5 días y 3 horas

# Restar un timedelta de una fecha
fecha_menos_dias = ahora - diferencia
print(fecha_menos_dias)  # Fecha actual menos 5 días y 3 horas
```

📌 **Explicación:**
- `timedelta` puede usarse para sumar o restar días, horas, minutos, etc., a un objeto `datetime`.
- Esto es útil cuando necesitas calcular fechas pasadas o futuras.

---

## 🔹 Comparaciones de Fechas

Las fechas en Python pueden ser comparadas directamente usando operadores de comparación (`<`, `>`, `==`).

### 🛠️ Ejemplo: Comparación de Fechas

```python
fecha1 = datetime(2025, 3, 11, 14, 30)
fecha2 = datetime(2025, 3, 12, 14, 30)

print(fecha1 < fecha2)  # True
print(fecha1 == fecha2)  # False
```

📌 **Explicación:**
- Los objetos `datetime` pueden compararse directamente para ver si una fecha es anterior o posterior a otra.

---

## 🔹 Manejo de Zonas Horarias (`timezone`)

El módulo `datetime` también permite trabajar con zonas horarias mediante la clase `timezone`.

### 🛠️ Ejemplo: Usar `timezone`

```python
from datetime import timezone, timedelta

# Crear un objeto timezone con un desplazamiento de +2 horas
zona_horaria = timezone(timedelta(hours=2))

# Asignar una zona horaria a un objeto datetime
fecha_con_zona = datetime(2025, 3, 11, 14, 30, tzinfo=zona_horaria)
print(fecha_con_zona)  # 2025-03-11 14:30:00+02:00
```

📌 **Explicación:**
- `timezone` permite asignar un desplazamiento de zona horaria a un objeto `datetime`.
- Puedes usar esta funcionalidad para manejar fechas con zonas horarias específicas.

---

## 🚀 Conclusión

- El módulo `datetime` es esencial para trabajar con fechas y horas en Python, especialmente en **Data Engineering**.
- Las operaciones con fechas y horas son fáciles de realizar mediante clases como `datetime`, `timedelta` y `timezone`.
- El formato y análisis de fechas es crucial para procesar datos de registros, timestamps y otros eventos temporales.
- **Usar correctamente las fechas** y realizar operaciones con `timedelta` y zonas horarias es fundamental para mantener la precisión temporal en tus aplicaciones.

📌 **El manejo eficiente de fechas es vital cuando trabajas con datos temporales, como logs y eventos, y el módulo `datetime` proporciona todas las herramientas necesarias para hacerlo de manera efectiva.**
