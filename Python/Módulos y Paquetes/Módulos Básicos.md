
Python incluye muchos módulos útiles listos para usar. Aquí están algunos de los más importantes:

---

## 🔹 `os` (Sistema Operativo)

Permite interactuar con el sistema de archivos y ejecutar comandos del sistema.

```python
import os

print(os.getcwd())  # Obtiene el directorio actual
os.mkdir("nueva_carpeta")  # Crea una carpeta
os.remove("archivo.txt")  # Elimina un archivo
```

---

## 🔹 `sys` (Sistema y argumentos)

Maneja argumentos de la línea de comandos y la configuración del sistema.

```python
import sys

print(sys.argv)  # Lista de argumentos pasados al script
print(sys.platform)  # Nombre del sistema operativo
sys.exit()  # Sale del programa
```

📌 **Ejemplo CLI:**  
Si ejecutamos:  
```
python script.py argumento1 argumento2
```
Entonces `sys.argv` contendrá:  
```python
['script.py', 'argumento1', 'argumento2']
```

---

## 🔹 `math` (Matemáticas avanzadas)

Funciones matemáticas como trigonometría, raíces y logaritmos.

```python
import math

print(math.pi)  # 3.141592653589793
print(math.sqrt(16))  # 4.0
print(math.sin(math.radians(90)))  # 1.0
```

---

## 🔹 `random` (Números aleatorios)

Genera valores aleatorios.

```python
import random

print(random.randint(1, 10))  # Número entero entre 1 y 10
print(random.choice(["rojo", "verde", "azul"]))  # Elige un elemento al azar
print(random.uniform(1, 5))  # Número decimal entre 1 y 5
```

---

## 🔹 `datetime` (Fechas y horas)

Manejo de fechas y horas.

```python
import datetime

ahora = datetime.datetime.now()
print(ahora)  # Fecha y hora actual

fecha = datetime.datetime(2025, 1, 1)
print(fecha.strftime("%d/%m/%Y"))  # Formato de fecha: "01/01/2025"
```

---

## 🔹 `time` (Manejo del tiempo)

Permite hacer pausas o medir tiempos.

```python
import time

print("Iniciando...")
time.sleep(2)  # Pausa de 2 segundos
print("Fin")
```

---

## 🔹 `json` (Manejo de JSON)

Convierte entre JSON y Python.

```python
import json

datos = {"nombre": "Juan", "edad": 30}
json_str = json.dumps(datos)  # Convierte a JSON
print(json_str)  # '{"nombre": "Juan", "edad": 30}'

python_dict = json.loads(json_str)  # Convierte de JSON a dict
print(python_dict["nombre"])  # "Juan"
```

---

## 🔹 `re` (Expresiones Regulares)

Permite buscar patrones en textos.

```python
import re

texto = "Mi correo es ejemplo@email.com"
patron = r"\w+@\w+\.\w+"

coincidencia = re.search(patron, texto)
if coincidencia:
    print(coincidencia.group())  # "ejemplo@email.com"
```

---

## 🔥 Resumen

| Módulo | Función |
|--------|---------|
| `os` | Manipula archivos y directorios |
| `sys` | Maneja argumentos del sistema |
| `math` | Funciones matemáticas avanzadas |
| `random` | Genera valores aleatorios |
| `datetime` | Trabaja con fechas y horas |
| `time` | Maneja pausas y tiempos |
| `json` | Convierte JSON a dict y viceversa |
| `re` | Expresiones regulares |

