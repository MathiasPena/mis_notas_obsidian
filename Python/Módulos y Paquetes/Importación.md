
Python permite organizar el código en **módulos** y **paquetes**, facilitando la reutilización. Se pueden importar módulos de varias formas.

---

## 🔹 `import nombre_modulo`

Importa el módulo completo, y se acceden a sus funciones con `modulo.nombre_funcion()`.

```python
import math
print(math.sqrt(25))  # 5.0
```

---

## 🔹 `from nombre_modulo import funcion`

Importa una función o variable específica del módulo.

```python
from math import sqrt
print(sqrt(25))  # 5.0
```

---

## 🔹 `from nombre_modulo import *` (No recomendado)

Importa todo el contenido del módulo, pero puede causar conflictos de nombres.

```python
from math import *
print(sqrt(16))  # 4.0
```

⚠️ **No recomendado** porque puede sobrescribir funciones con el mismo nombre.

---

## 🔹 `import nombre_modulo as alias`

Permite usar un alias más corto.

```python
import math as m
print(m.sqrt(25))  # 5.0
```

---

## 🔹 Importar un módulo propio

Se pueden importar archivos `.py` en el mismo directorio.

📂 **Estructura del proyecto**:

```
/mi_proyecto
│── principal.py
│── modulo_utilidades.py
```

`modulo_utilidades.py`:
```python
def saludar():
    return "¡Hola desde el módulo!"
```

`principal.py`:
```python
import modulo_utilidades
print(modulo_utilidades.saludar())  # ¡Hola desde el módulo!
```

---

## 🔹 `sys.path`: Importar módulos desde otra carpeta

Si un módulo está en otra carpeta, se puede añadir su ruta.

```python
import sys
sys.path.append("/ruta/del/modulo")
import modulo_externo
```

---

## 🔥 Resumen

| Forma de Importación | Uso |
|----------------------|-----|
| `import modulo` | Importa el módulo completo |
| `from modulo import funcion` | Importa solo una función/variable |
| `from modulo import *` | Importa todo (⚠️ no recomendado) |
| `import modulo as alias` | Importa con un alias |
| `sys.path.append(ruta)` | Permite importar desde otra ubicación |
