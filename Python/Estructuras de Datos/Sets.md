
## ¿Qué es un set?
Un **set** es una colección desordenada de elementos únicos.

## Crear un set
```python
# Con llaves
mi_set = {1, 2, 3, 4}

# Con la función set()
otro_set = set([1, 2, 2, 3, 4])  # Elimina duplicados
```

## Métodos principales

### Agregar elementos
```python
mi_set.add(5)  # Agrega un elemento
```

### Eliminar elementos
```python
mi_set.remove(3)  # Elimina 3, error si no existe
mi_set.discard(10)  # No da error si no existe
mi_set.pop()  # Elimina un elemento aleatorio
mi_set.clear()  # Vacía el set
```

### Operaciones de conjuntos
```python
A = {1, 2, 3}
B = {3, 4, 5}

A.union(B)  # {1, 2, 3, 4, 5}
A | B       # {1, 2, 3, 4, 5}

A.intersection(B)  # {3}
A & B              # {3}

A.difference(B)  # {1, 2}
A - B            # {1, 2}

A.symmetric_difference(B)  # {1, 2, 4, 5}
A ^ B                      # {1, 2, 4, 5}
```

### Otras operaciones
```python
len(mi_set)  # Número de elementos
1 in mi_set  # True si el elemento está en el set
mi_set.copy()  # Copia el set
```

## ¿Cuándo usar sets?
- Para eliminar duplicados de una lista.
- Cuando necesitas operaciones matemáticas de conjuntos.
- Para búsquedas rápidas (verificar pertenencia es más eficiente que en listas).
