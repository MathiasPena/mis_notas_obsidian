
### Búsqueda Binaria

La **búsqueda binaria** es un algoritmo eficiente para encontrar un elemento en una lista **ordenada**. Se basa en la idea de dividir repetidamente el espacio de búsqueda a la mitad, lo que permite reducir el número de comparaciones necesarias para encontrar el elemento. La búsqueda binaria tiene una complejidad temporal de **O(log n)**, lo que la hace mucho más eficiente que la búsqueda lineal **O(n)** cuando se trabaja con grandes volúmenes de datos.

### Funcionamiento de la Búsqueda Binaria

El algoritmo de búsqueda binaria funciona de la siguiente manera:

1. Comienza con el rango completo de la lista ordenada.
2. Compara el elemento que se está buscando con el valor en el punto medio de la lista.
3. Si el elemento es igual al valor en el medio, se ha encontrado el elemento.
4. Si el elemento es menor que el valor en el medio, la búsqueda continúa en la mitad izquierda de la lista.
5. Si el elemento es mayor que el valor en el medio, la búsqueda continúa en la mitad derecha de la lista.
6. El proceso se repite recursivamente en el subrango hasta encontrar el elemento o reducir el rango a cero.

### Implementación de la Búsqueda Binaria

#### Función Recursiva

```python
def busqueda_binaria_recursiva(lista, objetivo, bajo=0, alto=None):
    if alto is None:
        alto = len(lista) - 1
    
    if bajo > alto:
        return -1  # Elemento no encontrado

    medio = (bajo + alto) // 2
    if lista[medio] == objetivo:
        return medio  # Elemento encontrado
    elif lista[medio] < objetivo:
        return busqueda_binaria_recursiva(lista, objetivo, medio + 1, alto)  # Buscar en la mitad derecha
    else:
        return busqueda_binaria_recursiva(lista, objetivo, bajo, medio - 1)  # Buscar en la mitad izquierda
```

#### Función Iterativa

```python
def busqueda_binaria_iterativa(lista, objetivo):
    bajo, alto = 0, len(lista) - 1
    while bajo <= alto:
        medio = (bajo + alto) // 2
        if lista[medio] == objetivo:
            return medio  # Elemento encontrado
        elif lista[medio] < objetivo:
            bajo = medio + 1  # Buscar en la mitad derecha
        else:
            alto = medio - 1  # Buscar en la mitad izquierda
    return -1  # Elemento no encontrado
```

### Complejidad Temporal

- **Mejor caso**: **O(1)** (cuando el primer elemento comparado es el objetivo).
- **Peor caso**: **O(log n)** (en el caso de que se tenga que reducir el rango de búsqueda a la mitad repetidamente).
- **Caso promedio**: **O(log n)**.

El tiempo de ejecución de la búsqueda binaria es logarítmico, ya que en cada paso se reduce el rango de búsqueda a la mitad. Este comportamiento es significativamente más eficiente que la búsqueda lineal, que tiene una complejidad de **O(n)**.

### Ejemplo de Uso

Supongamos que tenemos una lista ordenada de números y queremos encontrar el índice del número 7.

```python
numeros = [1, 3, 5, 7, 9, 11, 13, 15]
resultado = busqueda_binaria_iterativa(numeros, 7)
print(resultado)  # 3
```

En este caso, la búsqueda binaria buscaría el número 7 en la lista ordenada. El índice de 7 es **3**.

### Resumen

| Operación            | Complejidad |
|----------------------|-------------|
| Búsqueda Binaria     | O(log n)    |
| Mejor caso           | O(1)        |
| Peor caso            | O(log n)    |

### Conclusión

La **búsqueda binaria** es una técnica eficiente para buscar elementos en listas ordenadas. Su **complejidad temporal** de **O(log n)** la convierte en una opción mucho más rápida que la búsqueda lineal, especialmente cuando se trabaja con grandes volúmenes de datos. Si necesitas realizar búsquedas en listas ordenadas, la búsqueda binaria es la opción más adecuada.
