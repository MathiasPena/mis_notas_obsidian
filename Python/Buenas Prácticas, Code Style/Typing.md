
El **tipado estático** (typing) en Python se introduce mediante anotaciones de tipos, lo cual proporciona una forma de indicar explícitamente los tipos de las variables, los parámetros de las funciones y los valores de retorno. Esto mejora la legibilidad del código y ayuda a detectar errores antes de ejecutar el programa, facilitando también el uso de herramientas de análisis estático.

### 🛠️ Tipos Comunes en Python

#### 1.1. **List**

El tipo `List` es utilizado para definir una lista de elementos de un tipo específico. Se utiliza la anotación `List[Tipo]`, donde `Tipo` es el tipo de los elementos dentro de la lista.

```python
from typing import List

def sumar_elementos(numeros: List[int]) -> int:
    return sum(numeros)
```

En este caso, `numeros` es una lista de enteros (`List[int]`), y la función retorna un entero (`int`).

#### 1.2. **Dict**

El tipo `Dict` se utiliza para describir un diccionario, donde puedes especificar el tipo de las **claves** y los **valores**. Se utiliza `Dict[ClaveTipo, ValorTipo]`, donde `ClaveTipo` y `ValorTipo` son los tipos de las claves y los valores del diccionario, respectivamente.

```python
from typing import Dict

def calcular_precio(productos: Dict[str, float]) -> float:
    return sum(productos.values())
```

En este caso, `productos` es un diccionario donde las claves son de tipo `str` (nombre del producto) y los valores son de tipo `float` (precio del producto).

#### 1.3. **Optional**

El tipo `Optional` se usa cuando un valor puede ser de un tipo específico o `None`. Es equivalente a escribir `Union[Tipo, None]`. Se utiliza cuando se espera que una variable o parámetro pueda tener un valor o pueda ser nulo (es decir, `None`).

```python
from typing import Optional

def obtener_nombre(nombre: Optional[str]) -> str:
    if nombre is None:
        return "Nombre desconocido"
    return nombre
```

En este caso, `nombre` puede ser un `str` o `None`, y la función devuelve un `str`. Si el nombre es `None`, devuelve un valor predeterminado.

---

### 🛠️ Otros Tipos Comunes

- **Tuple**: Utilizado para tuplas con un número fijo de elementos de tipos específicos.
  
  ```python
  from typing import Tuple

  def dividir(a: int, b: int) -> Tuple[int, int]:
      coc, rem = divmod(a, b)
      return coc, rem
  ```

- **Union**: Para cuando una variable puede ser uno de varios tipos.

  ```python
  from typing import Union

  def procesar_dato(dato: Union[int, str]) -> str:
      return str(dato)
  ```

- **Any**: Permite cualquier tipo, sin especificar uno concreto. Usado cuando no hay restricción de tipo.

  ```python
  from typing import Any

  def mostrar(dato: Any) -> None:
      print(dato)
  ```

---

## 🚀 Conclusión

El uso de **typing** en Python es una práctica útil para mejorar la legibilidad del código, evitar errores y aprovechar las herramientas de análisis estático. Aunque Python es dinámico, las anotaciones de tipos proporcionan una forma de expresar las expectativas sobre los tipos de las variables y los valores que manejan, lo que hace que el código sea más fácil de entender y mantener.
