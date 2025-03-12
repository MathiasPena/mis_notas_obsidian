
### Prototype Pattern para clonación de objetos

El **Prototype Pattern** es un patrón de diseño creacional que permite copiar objetos existentes sin que el código dependa de sus clases específicas. Se usa cuando la creación de un objeto es costosa o compleja. En lugar de instanciar nuevos objetos desde cero, se clonan desde un prototipo existente, evitando costosos cálculos o inicializaciones.

Python maneja la clonación de objetos con los métodos `copy.copy()` (copia superficial) y `copy.deepcopy()` (copia profunda) del módulo `copy`.

---

## Clonación con `copy.copy()` (shallow copy)

La copia **superficial** (`shallow copy`) crea un nuevo objeto, pero **las referencias a objetos mutables dentro del original permanecen compartidas**.

```python
import copy

class Prototipo:
    def __init__(self, nombre, datos):
        self.nombre = nombre
        self.datos = datos  # Lista mutable

    def clonar(self):
        return copy.copy(self)  # Clon superficial

# Objeto original
original = Prototipo("Ejemplo", [1, 2, 3])

# Clon
clon = original.clonar()

# Modificamos los datos en el clon
clon.datos.append(4)

print(original.datos)  # [1, 2, 3, 4] -> Se modificó en el original también
print(clon.datos)      # [1, 2, 3, 4]
```

🔹 Como la lista `datos` es mutable, la copia superficial mantiene la referencia al mismo objeto, afectando tanto al original como al clon.

---

## Clonación con `copy.deepcopy()` (deep copy)

La copia **profunda** (`deep copy`) crea un nuevo objeto **y también duplica los objetos mutables internos**, evitando compartir referencias.

```python
class Prototipo:
    def __init__(self, nombre, datos):
        self.nombre = nombre
        self.datos = datos  # Lista mutable

    def clonar_profundo(self):
        return copy.deepcopy(self)  # Clon profundo

# Objeto original
original = Prototipo("Ejemplo", [1, 2, 3])

# Clon profundo
clon_profundo = original.clonar_profundo()

# Modificamos los datos en el clon
clon_profundo.datos.append(4)

print(original.datos)       # [1, 2, 3] -> No se modifica el original
print(clon_profundo.datos)  # [1, 2, 3, 4]
```

🔹 Con `deepcopy()`, el clon tiene su propia copia de `datos`, por lo que cambiarlo no afecta al original.

---

## Implementación de Prototype Pattern con un Registro

Podemos usar un **registro de prototipos** para almacenar y reutilizar prototipos predefinidos.

```python
class PrototipoRegistry:
    def __init__(self):
        self.prototipos = {}

    def registrar(self, clave, prototipo):
        self.prototipos[clave] = prototipo

    def obtener_prototipo(self, clave):
        return self.prototipos[clave].clonar_profundo()

# Creación y registro de prototipos
registro = PrototipoRegistry()
registro.registrar("obj1", Prototipo("Modelo A", [10, 20, 30]))

# Obtener un clon del prototipo registrado
nuevo_objeto = registro.obtener_prototipo("obj1")
nuevo_objeto.datos.append(40)

print(registro.prototipos["obj1"].datos)  # [10, 20, 30]
print(nuevo_objeto.datos)                 # [10, 20, 30, 40]
```

🔹 Aquí usamos un diccionario para almacenar prototipos reutilizables y clonarlos bajo demanda.

---

## Cuándo usar Prototype Pattern

✅ Cuando la creación de objetos es costosa en términos de tiempo o recursos.  
✅ Cuando se necesita duplicar objetos sin acoplar el código a sus clases concretas.  
✅ Cuando se requiere un sistema flexible de creación de objetos dinámicos.  

Ejemplo de uso en **Data Engineering**:  
- Clonar configuraciones de procesamiento de datos sin definir cada una desde cero.  
- Crear múltiples instancias con pequeñas variaciones para pruebas A/B.  
- Duplicar modelos de datos o estructuras sin recalcularlas.

---

## Resumen

🔹 `copy.copy()` realiza una **copia superficial**, útil para objetos con solo datos inmutables.  
🔹 `copy.deepcopy()` crea una **copia profunda**, útil cuando hay estructuras mutables.  
🔹 Un **registro de prototipos** permite almacenar y reutilizar objetos base.  

El **Prototype Pattern** facilita la creación eficiente de copias de objetos sin modificar el original. 🚀
