
Los métodos son funciones definidas dentro de una clase que operan sobre sus instancias u objetos. Existen varios tipos de métodos, incluyendo los **especiales o dunder methods** (doble subrayado, como `__init__` y `__str__`).

---

## 1. Método `__init__` (Constructor)

Es el **constructor** de una clase, se ejecuta al crear un objeto e inicializa atributos:
```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad
```

Uso:
```python
p1 = Persona("Juan", 30)
print(p1.nombre)  # "Juan"
print(p1.edad)  # 30
```

---

## 2. Método `__str__` (Representación en String)

Define la representación del objeto al usar `print(objeto)` o `str(objeto)`.
```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad

    def __str__(self):
        return f"Persona: {self.nombre}, {self.edad} años"
```

```python
p1 = Persona("Ana", 25)
print(p1)  # "Persona: Ana, 25 años"
```

---

## 3. Método `__repr__` (Representación para Desarrolladores)

Similar a `__str__`, pero debe devolver una representación precisa del objeto, útil para depuración.
```python
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad

    def __repr__(self):
        return f'Persona("{self.nombre}", {self.edad})'
```

```python
p1 = Persona("Carlos", 40)
print(repr(p1))  # 'Persona("Carlos", 40)'
```

---

## 4. Método `__del__` (Destructor)

Se ejecuta cuando el objeto es eliminado con `del objeto` o cuando ya no hay referencias a él.
```python
class Ejemplo:
    def __init__(self, nombre):
        self.nombre = nombre
        print(f"Objeto {nombre} creado")

    def __del__(self):
        print(f"Objeto {self.nombre} eliminado")

obj = Ejemplo("A")  # "Objeto A creado"
del obj  # "Objeto A eliminado"
```

---

## 5. Otros Métodos Especiales Útiles

| Método | Descripción |
|--------|------------|
| `__len__(self)` | Define el comportamiento de `len(objeto)`. |
| `__call__(self, *args)` | Permite llamar a un objeto como función. |
| `__eq__(self, other)` | Define `obj1 == obj2`. |
| `__lt__(self, other)` | Define `obj1 < obj2`. |
| `__getitem__(self, key)` | Hace que el objeto se comporte como una lista o diccionario. |

### Ejemplo:
```python
class ListaNumeros:
    def __init__(self, numeros):
        self.numeros = numeros

    def __len__(self):
        return len(self.numeros)

    def __getitem__(self, index):
        return self.numeros[index]

    def __call__(self):
        return sum(self.numeros)

lista = ListaNumeros([1, 2, 3, 4, 5])
print(len(lista))  # 5
print(lista[2])  # 3
print(lista())  # 15 (suma de los números)
```

---

### 🔥 **Resumen Rápido**
✅ `__init__` → Constructor, inicializa atributos.  
✅ `__str__` → Representación en string para `print(objeto)`.  
✅ `__repr__` → Representación exacta para depuración.  
✅ `__del__` → Destructor, se ejecuta al eliminar el objeto.  
✅ Métodos especiales como `__len__`, `__call__`, `__getitem__`, etc., permiten comportamientos personalizados.  
