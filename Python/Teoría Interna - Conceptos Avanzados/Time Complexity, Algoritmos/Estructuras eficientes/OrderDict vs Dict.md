# Python para Data Engineering - Teoría Interna y Conceptos Avanzados

## 13. Estructuras eficientes para grandes volúmenes de datos

### OrderedDict vs dict

En Python, los diccionarios (`dict`) son estructuras de datos muy utilizadas para almacenar pares clave-valor. Sin embargo, el comportamiento de los diccionarios tradicionales ha cambiado en versiones recientes de Python, y ahora mantienen el orden de inserción de las claves. Aun así, existe una variante de diccionario llamada **`OrderedDict`** en el módulo `collections`, que ofrece algunas funcionalidades adicionales en cuanto al manejo del orden de los elementos.

### dict

En las versiones más antiguas de Python (antes de la 3.7), los diccionarios no mantenían el orden de inserción de las claves. Sin embargo, a partir de Python 3.7, los **diccionarios estándar** (`dict`) ahora mantienen el orden en que se insertan los elementos, aunque no garantizan un comportamiento tan robusto como el de `OrderedDict`.

#### Ejemplo de uso de `dict`

```python
my_dict = {'a': 1, 'b': 2, 'c': 3}
for key, value in my_dict.items():
    print(key, value)
# Salida:
# a 1
# b 2
# c 3
```

En este ejemplo, el diccionario mantiene el orden de inserción de las claves a partir de Python 3.7.

### OrderedDict

Un **`OrderedDict`** es una subclase de `dict` que garantiza el orden de los elementos según la inserción o las operaciones de modificación realizadas, como el movimiento de elementos dentro del diccionario.

#### Características adicionales de `OrderedDict`:
1. Permite mover elementos al principio o al final del diccionario utilizando métodos como `move_to_end()`.
2. Es útil cuando es necesario realizar operaciones que dependan explícitamente del orden de los elementos.

#### Ejemplo de uso de `OrderedDict`

```python
from collections import OrderedDict

ordered_dict = OrderedDict()
ordered_dict['a'] = 1
ordered_dict['b'] = 2
ordered_dict['c'] = 3

# Mostrar el orden de los elementos
for key, value in ordered_dict.items():
    print(key, value)
# Salida:
# a 1
# b 2
# c 3

# Mover 'b' al final
ordered_dict.move_to_end('b')

# Mostrar el nuevo orden
for key, value in ordered_dict.items():
    print(key, value)
# Salida:
# a 1
# c 3
# b 2
```

### Diferencias clave entre `dict` y `OrderedDict`

| Característica               | `dict` (Python 3.7+)         | `OrderedDict`               |
|------------------------------|-----------------------------|-----------------------------|
| Orden de inserción            | Sí, pero no garantiza orden en todas las operaciones | Sí, mantiene el orden de inserción y permite mover elementos |
| Funcionalidad extra           | No                         | Permite mover elementos al principio o al final, entre otras operaciones |
| Uso recomendado               | Diccionarios simples        | Cuando el orden es importante y se deben realizar operaciones de reordenamiento |
| Método `move_to_end()`        | No                         | Sí, permite mover un elemento al final o al principio |

### Casos de uso

- **`dict`**: Perfecto para casos en los que solo necesitas almacenar pares clave-valor y el orden de los elementos no es relevante, pero se prefiere mantener el orden de inserción desde Python 3.7.
  
- **`OrderedDict`**: Ideal cuando necesitas mantener el orden de inserción o realizar operaciones específicas como mover elementos al principio o al final del diccionario. Es útil en aplicaciones que requieren control sobre el orden de los elementos, como implementaciones de caches, registros de actividad o cuando se necesita asegurar un orden determinado en las claves.

### Resumen

1. **`dict`** es eficiente para almacenar datos sin importar el orden en el que se insertan, pero en Python 3.7 y versiones posteriores mantiene el orden de inserción.
2. **`OrderedDict`** ofrece una mayor flexibilidad con respecto al orden de los elementos y permite mover elementos al principio o al final, lo cual es útil en escenarios más complejos donde el orden es importante.

### Conclusión

Aunque **`dict`** ahora mantiene el orden de inserción a partir de Python 3.7, si necesitas realizar operaciones avanzadas sobre el orden de los elementos o manipular el orden de manera más controlada, **`OrderedDict`** es la opción indicada. Sin embargo, para la mayoría de los casos donde solo se necesita almacenar datos clave-valor y no se requiere una manipulación avanzada del orden, **`dict`** es suficiente y más eficiente.
