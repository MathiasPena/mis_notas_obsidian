# Python para Data Engineering - Buenas Prácticas y Code Style

## 1. SOLID en Python

**SOLID** es un acrónimo que representa cinco principios fundamentales del diseño orientado a objetos que ayudan a crear software más mantenible y escalable. Estos principios fueron introducidos por Robert C. Martin (también conocido como Uncle Bob) y se aplican en cualquier lenguaje orientado a objetos, incluido Python.

### 🛠️ 1.1. **Single Responsibility Principle (SRP)** - Principio de Responsabilidad Única

Cada clase debe tener una única responsabilidad, lo que significa que debe haber una única razón para cambiar una clase. Esto facilita la comprensión, el mantenimiento y la extensión del código.

#### Ejemplo:

```python
class Report:
    def generate_report(self):
        # Lógica para generar el reporte
        pass

class EmailSender:
    def send_email(self, report):
        # Lógica para enviar el reporte por email
        pass
```

En este caso, la clase `Report` se encarga solo de la generación de informes, y la clase `EmailSender` se encarga solo del envío de correos electrónicos. De esta forma, si el método de generación de reportes cambia, solo se modifica `Report`.

---

### 🛠️ 1.2. **Open/Closed Principle (OCP)** - Principio Abierto/Cerrado

Las clases deben estar abiertas para su extensión, pero cerradas para su modificación. Esto significa que puedes agregar funcionalidad a una clase sin modificar su código original.

#### Ejemplo:

```python
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side ** 2

def calculate_area(shape: Shape):
    return shape.area()
```

Aquí, las clases `Circle` y `Square` extienden la clase `Shape` sin modificarla. Puedes agregar nuevas formas en el futuro sin tocar la clase `Shape`.

---

### 🛠️ 1.3. **Liskov Substitution Principle (LSP)** - Principio de Sustitución de Liskov

Los objetos de una clase derivada deben ser sustituibles por objetos de la clase base sin alterar la funcionalidad del programa. Es decir, cualquier instancia de una clase base debería poder ser reemplazada por una instancia de una clase derivada sin causar errores.

#### Ejemplo:

```python
class Bird:
    def fly(self):
        pass

class Sparrow(Bird):
    def fly(self):
        print("El gorrión está volando")

class Penguin(Bird):
    def fly(self):
        raise NotImplementedError("Los pingüinos no pueden volar")

# Liskov Substitution Principle violado
def make_bird_fly(bird: Bird):
    bird.fly()

# Si pasas un objeto Penguin, esto generará un error
make_bird_fly(Sparrow())  # Funciona correctamente
make_bird_fly(Penguin())  # Error: NotImplementedError
```

El principio de Liskov se viola en este caso porque un `Penguin` no puede ser sustituido por un `Bird` sin causar un error. Una solución sería tener una jerarquía de clases más adecuada, tal vez separando a los pingüinos en una clase diferente sin heredar de `Bird`.

---

### 🛠️ 1.4. **Interface Segregation Principle (ISP)** - Principio de Segregación de Interfaces

Es mejor tener varias interfaces específicas en lugar de una interfaz general. Cada cliente debería depender solo de las interfaces que utiliza, evitando la implementación de métodos que no son necesarios.

#### Ejemplo:

```python
class Printer:
    def print_document(self, document):
        pass

    def scan_document(self, document):
        pass

class Scanner:
    def scan_document(self, document):
        pass

# Si una clase necesita solo la funcionalidad de impresión, no debería tener que implementar el método de escaneo
class SimplePrinter(Printer):
    def print_document(self, document):
        print(f"Imprimiendo {document}")
```

En este caso, si `SimplePrinter` solo necesita imprimir y no escanear, no es ideal que tenga que implementar el método `scan_document`. Para evitar esto, se podría separar la interfaz en interfaces más específicas.

---

### 🛠️ 1.5. **Dependency Inversion Principle (DIP)** - Principio de Inversión de Dependencias

Las clases de alto nivel no deben depender de las clases de bajo nivel, sino de abstracciones. Las abstracciones no deben depender de detalles. Los detalles deben depender de las abstracciones. Esto ayuda a desacoplar el código y facilita la extensión y la prueba.

#### Ejemplo:

```python
from abc import ABC, abstractmethod

class Database(ABC):
    @abstractmethod
    def save(self, data):
        pass

class MySQLDatabase(Database):
    def save(self, data):
        print("Guardando datos en MySQL")

class MongoDBDatabase(Database):
    def save(self, data):
        print("Guardando datos en MongoDB")

class DataManager:
    def __init__(self, database: Database):
        self.database = database

    def save_data(self, data):
        self.database.save(data)

# Usando el principio de inversión de dependencias
mysql_db = MySQLDatabase()
mongo_db = MongoDBDatabase()

data_manager = DataManager(mysql_db)
data_manager.save_data("Datos importantes")

data_manager = DataManager(mongo_db)
data_manager.save_data("Otros datos")
```

En este caso, `DataManager` depende de la abstracción `Database`, no de detalles específicos como `MySQLDatabase` o `MongoDBDatabase`. Esto permite cambiar la base de datos fácilmente sin modificar `DataManager`.

---

### 🚀 Conclusión

El principio **SOLID** es esencial para escribir código limpio y mantenible. Aplicar estos principios en Python ayuda a mejorar la extensibilidad, la reutilización y la comprensión del código. Al adherirse a SOLID, se facilita la evolución del software y se reduce la probabilidad de errores y refactorizaciones costosas en el futuro.
