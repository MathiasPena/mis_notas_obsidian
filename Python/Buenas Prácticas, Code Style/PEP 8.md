# Python para Data Engineering - Buenas Prácticas y Code Style

## 1. PEP 8 (Estilo de Código)

**PEP 8** es la guía oficial de estilo de código para Python. Define cómo debe estructurarse el código Python para ser más legible, coherente y fácil de mantener. Esta convención es seguida por la mayoría de los desarrolladores Python y es crucial para mejorar la calidad del código, especialmente en proyectos colaborativos.

---

## 🔹 Principales Reglas de PEP 8

### 🛠️ 1. Nombres de Variables y Funciones

- **Usar minúsculas con guiones bajos** (snake_case) para nombres de variables, funciones y métodos.
  
```python
# Correcto
variable_ejemplo = 5
def calcular_area():
    pass

# Incorrecto
VariableEjemplo = 5
def CalcularArea():
    pass
```

### 🛠️ 2. Nombres de Clases

- **Usar mayúsculas con notación PascalCase** para nombres de clases.

```python
# Correcto
class MiClase:
    pass

# Incorrecto
class miClase:
    pass
```

### 🛠️ 3. Constantes

- **Usar mayúsculas y guiones bajos** (UPPERCASE_WITH_UNDERSCORES) para constantes.

```python
# Correcto
PI = 3.14
MAXIMO = 100

# Incorrecto
Pi = 3.14
Maximo = 100
```

---

## 🔹 Espaciado y Organización

### 🛠️ 4. Indentación

- **Usar 4 espacios por nivel de indentación** en lugar de tabulaciones.
  
```python
# Correcto
def funcion_ejemplo():
    if True:
        print("Hola Mundo")

# Incorrecto
def funcion_ejemplo():
→if True:
→→print("Hola Mundo")
```

### 🛠️ 5. Líneas en blanco

- **Usar una línea en blanco** para separar funciones y clases dentro de una clase o módulo.
- **Usar dos líneas en blanco** para separar clases y funciones al nivel del módulo.

```python
# Correcto
class MiClase:
    def metodo_uno(self):
        pass

    def metodo_dos(self):
        pass


def funcion_global():
    pass

# Incorrecto
class MiClase:
    def metodo_uno(self):
        pass
    def metodo_dos(self):
        pass


def funcion_global():
    pass
```

### 🛠️ 6. Líneas de código

- **Limitar las líneas de código a 79 caracteres** como máximo. Las líneas de comentarios deben ser de un máximo de 72 caracteres.

```python
# Correcto
print("Este es un mensaje que no supera los 79 caracteres.")
```

---

## 🔹 Comentarios

### 🛠️ 7. Comentarios en el Código

- Los comentarios deben ser **claros y útiles**.
- Usa comentarios para explicar el "por qué" del código, no lo que hace (eso debe ser obvio a partir del código mismo).
- Los comentarios deben empezar con **letra mayúscula** y terminar con **punto**.
- Usa comentarios en línea con moderación.

```python
# Correcto
# Esta función calcula el área de un círculo dado su radio.
def calcular_area_circulo(radio):
    return 3.14 * radio ** 2

# Incorrecto
#calcular_area_circulo(radio)
```

---

## 🔹 Importaciones

### 🛠️ 8. Orden de las Importaciones

- **Importaciones estándar** (como `os`, `sys`) deben ir primero.
- **Importaciones de terceros** (como `numpy`, `pandas`) van después.
- **Importaciones locales** (como módulos creados por el usuario) van al final.
  
Además, separa cada grupo con una línea en blanco.

```python
# Correcto
import os
import sys

import numpy as np
import pandas as pd

from mi_modulo import MiClase

# Incorrecto
import numpy as np
import sys
import os
```

### 🛠️ 9. Importar funciones específicas

- **Usa importaciones explícitas** para evitar importar todo el módulo si solo necesitas ciertas funciones.

```python
# Correcto
from math import pi, sqrt

# Incorrecto
import math
```

---

## 🔹 Otras Buenas Prácticas

### 🛠️ 10. Evitar Código Duplicado

- **No repitas código**. Si encuentras que una sección de código se repite en varios lugares, considera convertirla en una función o clase reutilizable.

### 🛠️ 11. Manejo de Excepciones

- **Usa excepciones de manera apropiada**. No uses excepciones para control de flujo normal. Maneja las excepciones de forma específica.

```python
# Correcto
try:
    valor = int(input("Introduce un número: "))
except ValueError:
    print("Eso no es un número válido")

# Incorrecto
try:
    # Código que podría lanzar una excepción
    pass
except:
    pass
```

---

## 🚀 Conclusión

Seguir **PEP 8** es fundamental para escribir código Python limpio, legible y mantenible. Implementar estas buenas prácticas no solo mejora la calidad del código, sino que facilita el trabajo en equipo, la depuración y la ampliación de proyectos. Si trabajas en proyectos colaborativos o de gran escala, asegúrate de seguir estas convenciones para evitar problemas a largo plazo.

📌 **PEP 8 no es solo una guía de estilo, sino una filosofía para hacer que tu código sea más claro y consistente.**
