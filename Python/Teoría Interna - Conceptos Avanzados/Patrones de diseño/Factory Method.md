
### Factory Method

El **Factory Method** es un patrón de diseño creacional que proporciona una interfaz para crear objetos en una superclase, pero permite que las subclases alteren el tipo de objetos que se crean. Se usa cuando no se sabe de antemano qué tipo exacto de objeto se debe crear o cuando la lógica de creación debe mantenerse separada del código cliente.

Este patrón es útil en Python para mejorar la flexibilidad y desacoplar la creación de objetos de su uso.

---

## Implementación del Factory Method en Python

### 1. Definición de una Clase Base

```python
from abc import ABC, abstractmethod

class Transporte(ABC):
    """Clase base abstracta para definir un tipo de transporte."""

    @abstractmethod
    def entregar(self):
        pass
```

Aquí, `Transporte` es una clase abstracta que define un método `entregar()`, el cual debe ser implementado por todas las subclases.

---

### 2. Creación de Clases Concretas

```python
class Camion(Transporte):
    """Implementación de un transporte terrestre."""
    
    def entregar(self):
        return "Entrega por camión."

class Barco(Transporte):
    """Implementación de un transporte marítimo."""
    
    def entregar(self):
        return "Entrega por barco."
```

Las clases `Camion` y `Barco` heredan de `Transporte` e implementan el método `entregar()` de manera diferente.

---

### 3. Implementación del Factory Method

```python
class TransporteFactory:
    """Factory Method para crear instancias de transporte."""

    @staticmethod
    def crear_transporte(tipo):
        if tipo == "camion":
            return Camion()
        elif tipo == "barco":
            return Barco()
        else:
            raise ValueError("Tipo de transporte desconocido.")
```

Aquí, `crear_transporte()` es el método de fábrica que devuelve una instancia del tipo de transporte deseado.

---

### 4. Uso del Factory Method

```python
# Crear transportes usando la fábrica
transporte1 = TransporteFactory.crear_transporte("camion")
transporte2 = TransporteFactory.crear_transporte("barco")

print(transporte1.entregar())  # Output: "Entrega por camión."
print(transporte2.entregar())  # Output: "Entrega por barco."
```

Este enfoque permite que el código cliente use el Factory Method sin conocer las clases concretas.

---

## Ventajas del Factory Method

✅ **Desacoplamiento**: El código cliente no necesita conocer las clases concretas ni cómo se crean.  
✅ **Extensibilidad**: Se pueden agregar nuevas subclases sin modificar el código existente.  
✅ **Mantenimiento más fácil**: La lógica de creación de objetos está centralizada en un solo lugar.  

---

## Casos de Uso Comunes

- **Conexiones a bases de datos**: Crear diferentes conexiones según el tipo de base de datos (`MySQL`, `PostgreSQL`, `SQLite`).
- **Creación de controladores de API**: Retornar diferentes instancias según el servicio de terceros que se utilice.
- **Interfaces gráficas**: Crear distintos componentes según el sistema operativo (Windows, macOS, Linux).

---

## Resumen

El **Factory Method** en Python es un patrón de diseño útil para crear objetos de manera flexible y desacoplada. Permite definir una interfaz común para la creación de objetos y delegar la implementación a subclases o métodos de fábrica. Su uso es ideal cuando se necesita mayor flexibilidad en la creación de objetos sin acoplar el código cliente a clases concretas.
