
Python es un lenguaje orientado a objetos, lo que significa que todo en Python es un objeto. Se pueden crear **clases** para definir estructuras y **objetos** como instancias de esas clases.

---

## 1. Definición de una Clase

Una clase se define con la palabra clave `class`:
```python
class Persona:
    pass  # Clase vacía
```

Se pueden definir **atributos y métodos** dentro de la clase:

```python
class Persona:
    def __init__(self, nombre, edad):  # Constructor
        self.nombre = nombre  # Atributo de instancia
        self.edad = edad

    def saludar(self):  # Método
        return f"Hola, soy {self.nombre} y tengo {self.edad} años."
```

---

## 2. Creación de un Objeto

Un objeto es una instancia de una clase:
```python
p1 = Persona("Juan", 30)  # Crear objeto
print(p1.nombre)  # Acceder a un atributo → "Juan"
print(p1.saludar())  # Llamar a un método → "Hola, soy Juan y tengo 30 años."
```

Cada objeto tiene sus propios valores de atributos:
```python
p2 = Persona("Ana", 25)
print(p2.saludar())  # "Hola, soy Ana y tengo 25 años."
```

---

## 3. Atributos de Instancia y de Clase

### **Atributos de Instancia (propios de cada objeto)**
Se definen en el constructor (`__init__`):
```python
class Perro:
    def __init__(self, nombre):
        self.nombre = nombre  # Cada objeto tendrá su propio "nombre"
```
```python
p1 = Perro("Rex")
p2 = Perro("Luna")
print(p1.nombre)  # "Rex"
print(p2.nombre)  # "Luna"
```

### **Atributos de Clase (compartidos por todos los objetos)**
Se definen fuera del `__init__` y son iguales para todas las instancias:
```python
class Perro:
    especie = "Canino"  # Atributo de clase

    def __init__(self, nombre):
        self.nombre = nombre  # Atributo de instancia
```
```python
p1 = Perro("Rex")
print(p1.especie)  # "Canino"
print(Perro.especie)  # "Canino"
```

---

## 4. Métodos de Clase, Estáticos y de Instancia

| Método | Definición | Uso |
|--------|-----------|-----|
| Método de instancia | `def metodo(self):` | Usa `self` y accede a atributos de instancia. |
| Método de clase | `@classmethod` `def metodo(cls):` | Usa `cls` y accede a atributos de clase. |
| Método estático | `@staticmethod` `def metodo():` | No usa `self` ni `cls`, es una función dentro de la clase. |

### **Ejemplo de cada tipo:**
```python
class Ejemplo:
    atributo_clase = "Valor de clase"

    def __init__(self, valor):
        self.atributo_instancia = valor

    def metodo_instancia(self):
        return f"Instancia: {self.atributo_instancia}"

    @classmethod
    def metodo_clase(cls):
        return f"Clase: {cls.atributo_clase}"

    @staticmethod
    def metodo_estatico():
        return "Este es un método estático"
```

```python
obj = Ejemplo("Valor de instancia")
print(obj.metodo_instancia())  # "Instancia: Valor de instancia"
print(Ejemplo.metodo_clase())  # "Clase: Valor de clase"
print(Ejemplo.metodo_estatico())  # "Este es un método estático"
```

---

## 5. Modificadores de Acceso: Público, Protegido y Privado

Python no tiene modificadores como `private` o `protected` explícitos, pero usa convenciones:

| Tipo | Sintaxis | Accesible desde |
|------|---------|----------------|
| Público | `self.atributo` | Cualquier parte del código |
| Protegido | `self._atributo` | Convención: Solo dentro de la clase o subclases |
| Privado | `self.__atributo` | Convención: No debe ser accedido fuera de la clase |

Ejemplo:
```python
class Ejemplo:
    def __init__(self):
        self.publico = "Visible"
        self._protegido = "Convención: no modificar directamente"
        self.__privado = "Oculto"

    def mostrar_privado(self):
        return self.__privado  # Se puede acceder dentro de la clase
```

```python
obj = Ejemplo()
print(obj.publico)  # "Visible"
print(obj._protegido)  # "Convención: no modificar directamente"
# print(obj.__privado)  # ❌ Error (atributo privado)
print(obj.mostrar_privado())  # ✅ Se accede a __privado desde un método de la clase
```

---

## 6. Destructores (`__del__`)

El método `__del__` se ejecuta cuando un objeto es eliminado de la memoria:

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

### 🔥 **Resumen Rápido**
✅ **Clase:** Define la estructura (`class MiClase:`).  
✅ **Objeto:** Instancia de una clase (`obj = MiClase()`).  
✅ **`__init__`**: Constructor, inicializa atributos.  
✅ **Atributos de instancia:** `self.atributo`, únicos para cada objeto.  
✅ **Atributos de clase:** `atributo_clase`, compartidos por todas las instancias.  
✅ **Métodos de instancia:** Tienen `self`, acceden a atributos de instancia.  
✅ **Métodos de clase (`@classmethod`)**: Usan `cls`, acceden a atributos de clase.  
✅ **Métodos estáticos (`@staticmethod`)**: No dependen de instancias ni clases.  
✅ **Modificadores:** Público (`self.atributo`), Protegido (`self._atributo`), Privado (`self.__atributo`).  
✅ **Destructor (`__del__`)**: Se ejecuta al eliminar un objeto.  
