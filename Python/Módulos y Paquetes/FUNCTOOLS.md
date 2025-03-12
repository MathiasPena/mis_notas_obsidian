

El módulo `functools` proporciona herramientas para trabajar con funciones de manera más eficiente, permitiendo optimizar su rendimiento y crear versiones de ellas con argumentos predeterminados. Dos funciones muy útiles dentro de `functools` son **`lru_cache`** y **`partial`**.

---

## 🔹 ¿Qué es `functools`?

El módulo `functools` contiene una serie de funciones de orden superior que actúan sobre funciones o son útiles para optimizar y mejorar el comportamiento de las mismas. Se utiliza principalmente para **memoización**, **funciones parciales**, y otras técnicas de optimización.

---

## 🔹 `functools.lru_cache` - Caché de Resultados

`lru_cache` es un decorador que permite **almacenar en caché** los resultados de las funciones para evitar recalcular valores que ya han sido procesados previamente. Esto es útil para funciones costosas que se llaman repetidamente con los mismos parámetros.

### 🛠️ Ejemplo: Uso de `lru_cache`

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def calcular_fibonacci(n):
    if n <= 1:
        return n
    return calcular_fibonacci(n - 1) + calcular_fibonacci(n - 2)

# Llamadas rápidas con resultados almacenados en caché
print(calcular_fibonacci(10))  # Resultado calculado y almacenado
print(calcular_fibonacci(10))  # Resultado obtenido desde caché
```

📌 **Explicación:**
- `@lru_cache(maxsize=128)` almacena hasta 128 resultados. Si el número de resultados almacenados excede este límite, el menos reciente (Least Recently Used) se elimina.
- Es útil cuando la función tiene cálculos repetidos con los mismos argumentos.

---

## 🔹 `functools.partial` - Funciones Parciales

`partial` es una función que permite **fijar ciertos argumentos de una función**. Puedes crear nuevas funciones a partir de funciones existentes, pero con algunos argumentos predeterminados, lo que facilita su reutilización.

### 🛠️ Ejemplo: Uso de `partial`

```python
from functools import partial

# Definir una función simple
def multiplicar(a, b):
    return a * b

# Crear una nueva función parcial con el primer argumento fijo
doblar = partial(multiplicar, 2)

# Usar la función parcial
print(doblar(5))  # 2 * 5 = 10
```

📌 **Explicación:**
- `partial(multiplicar, 2)` crea una nueva función `doblar` que siempre multiplicará por 2. Luego, puedes pasar solo el segundo argumento.

---

## 🔹 Otras Funciones de `functools`

1. **`functools.reduce()`**: Aplica una función acumulativa a los elementos de un iterable, reduciéndolos a un único valor.
   
   ```python
   from functools import reduce
   
   # Sumar todos los elementos de una lista
   lista = [1, 2, 3, 4]
   resultado = reduce(lambda x, y: x + y, lista)
   print(resultado)  # 10
   ```

2. **`functools.wraps()`**: Utilizado para conservar la información de la función original cuando se usa un decorador, como su nombre y documentación.
   
   ```python
   from functools import wraps

   def decorador(func):
       @wraps(func)
       def wrapper(*args, **kwargs):
           return func(*args, **kwargs)
       return wrapper
   ```

---

## 🚀 Conclusión

- `functools` es una herramienta poderosa para optimizar y reutilizar funciones en Python.
- **`lru_cache`** te permite mejorar el rendimiento de funciones repetitivas mediante caché.
- **`partial`** facilita la creación de funciones más específicas a partir de funciones generales, reduciendo el código repetido.
- Otras funciones como `reduce` y `wraps` también son útiles para manipular y mejorar las funciones en tus programas.

📌 **Usar `functools` adecuadamente puede hacer que tu código sea más eficiente y fácil de mantener al evitar cálculos innecesarios y reducir la repetición.**
