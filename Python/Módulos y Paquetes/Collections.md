

El módulo `collections` ofrece una serie de tipos de datos especializados que proporcionan soluciones eficientes para manipular y almacenar datos de manera más eficaz que las estructuras estándar de Python.

---

## 🔹 ¿Qué es `collections`?

El módulo `collections` proporciona alternativas a las estructuras de datos estándar de Python (listas, diccionarios, tuplas) que están optimizadas para tareas comunes en el desarrollo de software, como contar elementos, gestionar valores predeterminados o crear tuplas con nombres.

---

## 🔹 `collections.Counter` - Contador de Elementos

`Counter` es una subclase de `dict` diseñada para contar elementos en un iterable. Es útil cuando se necesita saber cuántas veces aparece un elemento.

### 🛠️ Ejemplo: Uso de `Counter`

```python
from collections import Counter

# Contar elementos en una lista
contador = Counter(['a', 'b', 'c', 'a', 'b', 'a'])
print(contador)  # Counter({'a': 3, 'b': 2, 'c': 1})

# Contar caracteres en un string
contador_str = Counter("banana")
print(contador_str)  # Counter({'a': 3, 'n': 2, 'b': 1})

# Métodos útiles
print(contador.most_common(1))  # [('a', 3)]
```

📌 **Explicación:**
- `Counter` automáticamente cuenta las ocurrencias de cada elemento del iterable.
- `most_common(n)` devuelve los `n` elementos más comunes y sus frecuencias.

---

## 🔹 `collections.defaultdict` - Diccionario con Valores Predeterminados

`defaultdict` es una subclase de `dict` que proporciona un valor predeterminado para claves que no existen en el diccionario. Esto evita tener que comprobar si una clave está presente antes de acceder a ella.

### 🛠️ Ejemplo: Uso de `defaultdict`

```python
from collections import defaultdict

# Crear un defaultdict con valor predeterminado de tipo lista
diccionario = defaultdict(list)

# Agregar elementos sin preocuparnos si la clave existe
diccionario['a'].append(1)
diccionario['b'].append(2)
diccionario['a'].append(3)

print(diccionario)  # defaultdict(<class 'list'>, {'a': [1, 3], 'b': [2]})
```

📌 **Explicación:**
- En lugar de obtener un `KeyError` cuando se accede a una clave no existente, `defaultdict` devuelve un valor predeterminado, como una lista vacía en este caso.

---

## 🔹 `collections.namedtuple` - Tupla con Nombres de Campo

`namedtuple` permite crear tuplas con campos accesibles por nombre, lo que hace que el código sea más legible y fácil de mantener.

### 🛠️ Ejemplo: Uso de `namedtuple`

```python
from collections import namedtuple

# Crear una tupla con campos nombrados
Persona = namedtuple('Persona', ['nombre', 'edad'])

# Crear un objeto de tipo Persona
persona1 = Persona(nombre="Juan", edad=30)

print(persona1.nombre)  # Juan
print(persona1.edad)    # 30
```

📌 **Explicación:**
- `namedtuple` define una nueva clase de tupla donde puedes acceder a los campos por nombre en lugar de por índice, haciendo el código más claro y fácil de entender.

---

## 🔹 `collections.deque` - Cola de doble extremo

`deque` es una lista optimizada para **agregar y eliminar elementos** desde ambos extremos de manera eficiente (O(1) para ambas operaciones), lo que la hace ideal para implementaciones de colas y pilas.

### 🛠️ Ejemplo: Uso de `deque`

```python
from collections import deque

# Crear una deque
cola = deque([1, 2, 3])

# Agregar elementos a ambos extremos
cola.append(4)        # Cola: [1, 2, 3, 4]
cola.appendleft(0)    # Cola: [0, 1, 2, 3, 4]

# Eliminar elementos de ambos extremos
cola.pop()            # Cola: [0, 1, 2, 3]
cola.popleft()        # Cola: [1, 2, 3]

print(cola)           # deque([1, 2, 3])
```

📌 **Explicación:**
- `deque` permite realizar operaciones de agregar o quitar elementos de forma eficiente en ambos extremos.
- Es útil para implementar colas, pilas y otras estructuras de datos que requieren inserciones y eliminaciones rápidas.

---

## 🚀 Conclusión

- **`Counter`** es perfecto para contar elementos y frecuencias.
- **`defaultdict`** facilita trabajar con diccionarios al proporcionar valores predeterminados.
- **`namedtuple`** mejora la legibilidad del código al permitir el acceso a tuplas mediante nombres en lugar de índices.
- **`deque`** es ideal para tareas que requieren agregar o eliminar elementos rápidamente en ambos extremos.

📌 **El módulo `collections` proporciona estructuras de datos optimizadas que pueden mejorar significativamente la eficiencia y legibilidad de tu código.**
