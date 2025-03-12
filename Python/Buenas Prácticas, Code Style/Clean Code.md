
**Clean Code** (código limpio) es un conjunto de principios y mejores prácticas para escribir código legible, mantenible y de alta calidad. Estas prácticas no solo mejoran la comprensión del código, sino que también facilitan su depuración, prueba y ampliación. A continuación, se detallan las mejores prácticas específicas para escribir código limpio en Python.

### 🧹 1.1. **Nombres Claros y Descriptivos**

Los nombres de variables, funciones y clases deben ser descriptivos y expresar claramente su propósito.

#### Ejemplo:

```python
# Malo
def calc(a, b):
    return a + b

# Bueno
def calculate_sum(first_number, second_number):
    return first_number + second_number
```

El nombre `calculate_sum` es más descriptivo que `calc`, lo que facilita comprender la función de inmediato.

---

### 🧹 1.2. **Funciones Cortas y Simples**

Cada función debe hacer una sola cosa, y esa cosa debe ser claramente identificable. Las funciones largas son más difíciles de leer y comprender.

#### Ejemplo:

```python
# Malo
def process_data(data):
    cleaned_data = clean_data(data)
    filtered_data = filter_data(cleaned_data)
    analyzed_data = analyze_data(filtered_data)
    generate_report(analyzed_data)

# Bueno
def clean_data(data):
    # Limpia los datos
    pass

def filter_data(data):
    # Filtra los datos
    pass

def analyze_data(data):
    # Analiza los datos
    pass

def process_data(data):
    cleaned_data = clean_data(data)
    filtered_data = filter_data(cleaned_data)
    analyzed_data = analyze_data(filtered_data)
    generate_report(analyzed_data)
```

Dividir las funciones largas en funciones más pequeñas permite que cada una se enfoque en una tarea específica, lo que mejora la legibilidad.

---

### 🧹 1.3. **Evitar Comentarios Innecesarios**

El código debe ser lo suficientemente claro como para que no necesite comentarios excesivos. Si el código requiere muchos comentarios para entenderlo, eso podría indicar que el código no está lo suficientemente claro.

#### Ejemplo:

```python
# Malo
def calculate_area(radius):
    # Multiplicamos pi por el radio al cuadrado
    return 3.14 * radius ** 2

# Bueno
def calculate_area(radius):
    return 3.14 * radius ** 2
```

Los comentarios son útiles cuando son necesarios, pero deben evitarse en exceso. El código mismo debe hablar por sí mismo.

---

### 🧹 1.4. **Evitar Código Muerto**

El código no utilizado o no necesario debe eliminarse para evitar confusión y aumentar la mantenibilidad.

#### Ejemplo:

```python
# Malo
def calculate_area(radius):
    # Esta variable no se utiliza
    unused_variable = 10
    return 3.14 * radius ** 2

# Bueno
def calculate_area(radius):
    return 3.14 * radius ** 2
```

Eliminar código muerto mejora la claridad y el rendimiento del programa.

---

### 🧹 1.5. **Usar Excepciones de Forma Correcta**

Las excepciones deben usarse para manejar errores, no para el control de flujo. Esto hace que el código sea más robusto y fácil de seguir.

#### Ejemplo:

```python
# Malo
def find_value_in_list(value, my_list):
    try:
        return my_list.index(value)
    except ValueError:
        return -1

# Bueno
def find_value_in_list(value, my_list):
    if value in my_list:
        return my_list.index(value)
    return -1
```

Las excepciones deben manejarse solo cuando realmente ocurren errores, no como una forma de controlar el flujo de ejecución.

---

### 🧹 1.6. **Evitar Funciones con Muchos Parámetros**

Las funciones con muchos parámetros son difíciles de entender y usar correctamente. Si una función tiene más de tres o cuatro parámetros, probablemente es una señal de que debería dividirse o utilizarse un objeto para agrupar la información.

#### Ejemplo:

```python
# Malo
def create_user(name, age, email, address, phone_number):
    # Crea un usuario
    pass

# Bueno
class User:
    def __init__(self, name, age, email, address, phone_number):
        self.name = name
        self.age = age
        self.email = email
        self.address = address
        self.phone_number = phone_number

def create_user(user: User):
    # Crea un usuario
    pass
```

Al encapsular los parámetros dentro de una clase, el código se vuelve más manejable y fácil de entender.

---

### 🧹 1.7. **Evitar Uso Excesivo de Estructuras de Control**

El uso de estructuras de control como `if`, `else`, y `for` deben ser mínimos y deben ayudar a hacer el código más claro, no más complejo.

#### Ejemplo:

```python
# Malo
def calculate_discount(price, is_member, is_special_day):
    if is_member:
        price = price * 0.9
    if is_special_day:
        price = price * 0.8
    return price

# Bueno
def calculate_discount(price, discount_percentage):
    return price * (1 - discount_percentage)

def apply_member_discount(price):
    return calculate_discount(price, 0.1)

def apply_special_day_discount(price):
    return calculate_discount(price, 0.2)
```

En lugar de manejar múltiples condiciones dentro de una función, puedes dividir el cálculo en varias funciones pequeñas y claras.

---

### 🧹 1.8. **Pruebas Automatizadas**

Es fundamental que el código esté acompañado de pruebas automatizadas que aseguren que el sistema funciona como se espera. El código limpio no es solo código que se lee bien, sino también código que es fácil de probar.

#### Ejemplo:

```python
import unittest

class TestMathFunctions(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(1, 2), 3)

    def test_subtract(self):
        self.assertEqual(subtract(2, 1), 1)

if __name__ == '__main__':
    unittest.main()
```

El uso de pruebas unitarias facilita la validación de las funcionalidades y ayuda a mantener la calidad del código a lo largo del tiempo.

---

### 🧹 1.9. **Usar Listas por Comprensión y Generadores**

Python ofrece características como listas por comprensión y generadores que pueden hacer el código más limpio y eficiente. 

#### Ejemplo:

```python
# Malo
numbers = []
for i in range(10):
    numbers.append(i ** 2)

# Bueno
numbers = [i ** 2 for i in range(10)]
```

Las listas por comprensión son más compactas, legibles y expresivas que los bucles tradicionales.

---

### 🚀 Conclusión

Escribir **Clean Code** en Python no solo mejora la legibilidad y mantenibilidad del código, sino que también facilita su extensión y prueba. Seguir estas buenas prácticas es esencial para cualquier desarrollador que quiera escribir código de alta calidad que sea fácil de entender, modificar y escalar.
