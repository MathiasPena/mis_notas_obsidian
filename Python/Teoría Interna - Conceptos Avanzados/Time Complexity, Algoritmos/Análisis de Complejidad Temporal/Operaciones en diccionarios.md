
### Diccionarios en Python

Un **diccionario** en Python es una estructura de datos de tipo **hash map**, que almacena pares clave-valor. Es una de las estructuras de datos más eficientes y se usa comúnmente cuando necesitas asociar valores a claves únicas. Los diccionarios están implementados de tal forma que las operaciones de búsqueda, inserción y eliminación son, en la mayoría de los casos, muy rápidas.

### Complejidad Temporal de las Operaciones Comunes

#### `get` (Acceder al valor de una clave)

- **Complejidad**: **O(1)** en el caso promedio.
- **Descripción**: El método `get` permite acceder a un valor asociado a una clave específica. En condiciones normales, las búsquedas de claves en un diccionario son de tiempo constante **O(1)**, gracias al uso de una tabla de hash. El tiempo de búsqueda es independiente del tamaño del diccionario.

```python
diccionario = {'a': 1, 'b': 2, 'c': 3}
valor = diccionario.get('b')  # O(1)
print(valor)  # 2
```

#### `set` (Asignar o modificar el valor de una clave)

- **Complejidad**: **O(1)** en el caso promedio.
- **Descripción**: El método `set` (o la asignación directa con `diccionario[clave] = valor`) es muy eficiente. Al igual que con el método `get`, la asignación de valores a claves se realiza en tiempo constante **O(1)** en el caso promedio debido a la estructura interna de los diccionarios (tabla hash).

```python
diccionario = {'a': 1, 'b': 2}
diccionario['c'] = 3  # O(1)
print(diccionario)  # {'a': 1, 'b': 2, 'c': 3}
```

#### `del` (Eliminar un par clave-valor)

- **Complejidad**: **O(1)** en el caso promedio.
- **Descripción**: Eliminar un par clave-valor mediante `del diccionario[clave]` es una operación de tiempo constante **O(1)** en el caso promedio. Sin embargo, es importante tener en cuenta que la operación puede ser más lenta si ocurre un **rebalanceo** en la tabla hash interna.

```python
diccionario = {'a': 1, 'b': 2}
del diccionario['b']  # O(1)
print(diccionario)  # {'a': 1}
```

#### `in` (Comprobar si una clave existe en el diccionario)

- **Complejidad**: **O(1)** en el caso promedio.
- **Descripción**: El operador `in` se utiliza para verificar si una clave está presente en un diccionario. Esta operación es de tiempo constante **O(1)** en la mayoría de los casos.

```python
diccionario = {'a': 1, 'b': 2}
existe = 'b' in diccionario  # O(1)
print(existe)  # True
```

### Peor Caso (O(n))

Aunque las operaciones comunes de acceso y asignación en un diccionario tienen una complejidad de **O(1)**, existen escenarios donde el rendimiento puede degradarse.

- **Peor caso de colisiones en la tabla de hash**: Si hay demasiadas colisiones (cuando diferentes claves tienen el mismo valor hash), las operaciones de búsqueda, inserción y eliminación pueden volverse más lentas, con una complejidad de **O(n)**, donde **n** es el número de elementos en el diccionario.
- **Rebalanceo de la tabla de hash**: En ciertos casos, cuando se añaden demasiados elementos al diccionario, puede ocurrir un **rebalanceo** interno de la tabla hash, lo que temporalmente puede causar que las operaciones se ralenticen.

### Resumen de Complejidad Temporal

| Operación            | Complejidad |
|----------------------|-------------|
| `get`                | O(1)        |
| `set`                | O(1)        |
| `del`                | O(1)        |
| `in`                 | O(1)        |
| Peor caso (colisiones y rebalanceo) | O(n)  |

### Conclusión

En general, los diccionarios en Python son una de las estructuras de datos más eficientes para trabajar con pares clave-valor. Las operaciones más comunes, como acceder a un valor mediante una clave (`get`), asignar un valor a una clave (`set`), eliminar pares clave-valor (`del`) y comprobar la existencia de una clave (`in`), tienen una complejidad temporal de **O(1)** en la mayoría de los casos.

Sin embargo, en situaciones donde se producen muchas colisiones en la tabla hash o cuando se realiza un rebalanceo, la complejidad temporal puede empeorar a **O(n)**. A pesar de esto, los diccionarios siguen siendo una opción excelente para manejar datos en Python debido a su eficiencia en la mayoría de las operaciones.
