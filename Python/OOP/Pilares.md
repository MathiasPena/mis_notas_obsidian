# 🔹 Programación Orientada a Objetos (POO) en Python

La **POO** es un paradigma de programación basado en clases y objetos. Python implementa este paradigma con **cuatro pilares fundamentales**:

1. **Abstracción**
2. **Encapsulamiento**
3. **Herencia**
4. **Polimorfismo**

---

## 1️⃣ Abstracción

La **abstracción** permite ocultar detalles internos de implementación y solo mostrar lo esencial. Se logra mediante **clases abstractas** o **métodos privados**.

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def hacer_sonido(self):
        pass  # Obliga a las subclases a definir este método

class Perro(Animal):
    def hacer_sonido(self):
        return "Guau!"

class Gato(Animal):
    def hacer_sonido(self):
        return "Miau!"
```

```python
p = Perro()
print(p.hacer_sonido())  # "Guau!"
```

✅ **Beneficio**: Se ocultan los detalles de implementación y solo se exponen las funcionalidades clave.

---

## 2️⃣ Encapsulamiento

El **encapsulamiento** restringe el acceso a ciertos atributos o métodos de un objeto. Se logra con:

- **Públicos** (`variable`) → Accesibles desde cualquier parte.
- **Protegidos** (`_variable`) → No deberían modificarse fuera de la clase.
- **Privados** (`__variable`) → Solo accesibles dentro de la clase.

```python
class CuentaBancaria:
    def __init__(self, saldo):
        self.__saldo = saldo  # Atributo privado

    def depositar(self, monto):
        self.__saldo += monto

    def retirar(self, monto):
        if monto <= self.__saldo:
            self.__saldo -= monto
        else:
            print("Saldo insuficiente")

    def mostrar_saldo(self):
        return self.__saldo
```

```python
cuenta = CuentaBancaria(1000)
cuenta.depositar(500)
print(cuenta.mostrar_saldo())  # 1500
# print(cuenta.__saldo)  # Error: atributo privado
```

✅ **Beneficio**: Protege los datos de accesos no deseados y asegura la integridad del objeto.

---

## 3️⃣ Herencia

La **herencia** permite que una clase derive de otra, reutilizando código.

```python
class Vehiculo:
    def __init__(self, marca):
        self.marca = marca

    def acelerar(self):
        return "Acelerando..."

class Coche(Vehiculo):
    def __init__(self, marca, modelo):
        super().__init__(marca)  # Llama al constructor de la clase padre
        self.modelo = modelo
```

```python
c = Coche("Toyota", "Corolla")
print(c.marca)  # "Toyota"
print(c.acelerar())  # "Acelerando..."
```

## Herencia Múltiple

Una clase puede heredar de varias clases.

```python
class Volador:
    def volar(self):
        return "Estoy volando"

class Nadador:
    def nadar(self):
        return "Estoy nadando"

class Pato(Volador, Nadador):
    pass

p = Pato()
print(p.volar())  # "Estoy volando"
print(p.nadar())  # "Estoy nadando"
```

> **Nota**: Si hay métodos con el mismo nombre en ambas clases padre, Python sigue el orden de herencia (MRO - Method Resolution Order).

✅ **Beneficio**: Evita la duplicación de código y facilita la reutilización.

---

## 4️⃣ Polimorfismo

El **polimorfismo** permite que el mismo método tenga diferentes comportamientos según la clase.

```python
class Ave:
    def hacer_sonido(self):
        return "Pío"

class Perro:
    def hacer_sonido(self):
        return "Guau!"

def hacer_sonar(animal):
    print(animal.hacer_sonido())

hacer_sonar(Ave())  # "Pío"
hacer_sonar(Perro())  # "Guau!"
```

> **Clave**: No importa el tipo del objeto, mientras tenga `hacer_sonido()`, la función lo puede usar.

✅ **Beneficio**: Permite usar objetos de distintas clases de manera uniforme.

---

## Métodos y Clases Abstractas

Las **clases abstractas** definen métodos que deben ser implementados por las subclases. Se usa el módulo `abc`.

```python
from abc import ABC, abstractmethod

class Figura(ABC):
    @abstractmethod
    def area(self):
        pass

class Cuadrado(Figura):
    def __init__(self, lado):
        self.lado = lado

    def area(self):
        return self.lado ** 2
```

```python
# f = Figura()  # Esto daría error, no se pueden instanciar clases abstractas
c = Cuadrado(4)
print(c.area())  # 16
```

---
## 🔥 Resumen Rápido

| Pilar | Descripción | Ejemplo |
|-------|------------|---------|
| **Abstracción** | Oculta detalles innecesarios y expone solo lo esencial. | Clases abstractas (`ABC`) |
| **Encapsulamiento** | Protege los datos con atributos privados. | `self.__saldo` en `CuentaBancaria` |
| **Herencia** | Reutiliza código entre clases. | `Coche` hereda de `Vehiculo` |
| **Polimorfismo** | Un mismo método tiene diferentes implementaciones. | `hacer_sonido()` en `Ave` y `Perro` |
