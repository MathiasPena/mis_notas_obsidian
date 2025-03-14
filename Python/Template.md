# Python Core - Data Engineering (Trainee Level)

## 1. Manejo de Variables y Tipos de Datos
```python
x = 10          # Entero
pi = 3.14       # Flotante
name = "Data"   # Cadena de texto
is_valid = True # Booleano
```

## 2. Estructuras de Datos
### Listas (List)
```python
numbers = [1, 2, 3, 4]
numbers.append(5)  # Agregar un elemento
numbers.pop()      # Eliminar el último elemento
```

### Tuplas (Tuple)
```python
tuple_data = (1, "data", 3.5)  # Inmutable
```

### Diccionarios (Dict)
```python
data_dict = {"name": "Alice", "age": 25}
data_dict["city"] = "New York"  # Agregar clave-valor
```

### Conjuntos (Set)
```python
unique_numbers = {1, 2, 3, 3, 4}  # {1, 2, 3, 4}
```

## 3. Control de Flujo
```python
if x > 5:
    print("Mayor que 5")
elif x == 5:
    print("Igual a 5")
else:
    print("Menor que 5")
```

### Bucles
```python
for i in range(5):
    print(i)

while x > 0:
    x -= 1
```

## 4. Funciones
```python
def add(a, b):
    return a + b

result = add(3, 5)
```

## 5. Manejo de Archivos
```python
with open("data.txt", "r") as file:
    content = file.read()
```

## 6. Manejo de Errores
```python
try:
    x = 1 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
```

## 7. Programación Orientada a Objetos (OOP)
```python
class DataEngineer:
    def __init__(self, name):
        self.name = name
    
    def work(self):
        return f"{self.name} is processing data."

de = DataEngineer("Alice")
print(de.work())
```

## 8. Módulos y Librerías
```python
import os
import sys
import json
```

## 9. Manejo de Procesos y Concurrencia
### Threading
```python
import threading

def task():
    print("Task running")

thread = threading.Thread(target=task)
thread.start()
```

### Multiprocessing
```python
import multiprocessing

def process_task():
    print("Processing task")

process = multiprocessing.Process(target=process_task)
process.start()
```

## 10. Logging
```python
import logging
logging.basicConfig(level=logging.INFO)
logging.info("Data pipeline started")
```

## 11. Tipado Estático con Typing
```python
from typing import List, Dict

def process_data(data: List[int]) -> Dict[str, int]:
    return {"sum": sum(data)}
```
