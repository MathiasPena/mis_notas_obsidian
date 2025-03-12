
### Introducción

El **ordenamiento** es uno de los problemas fundamentales en la informática y es utilizado en una variedad de algoritmos y aplicaciones. Existen varios algoritmos de ordenamiento, pero dos de los más eficientes en cuanto a complejidad temporal son **Quicksort** y **Mergesort**, ambos con una complejidad de **O(n log n)** en el caso promedio.

### Quicksort

El **Quicksort** es un algoritmo de ordenamiento basado en la técnica de **divide y vencerás**. La idea es seleccionar un elemento como **pivote** y particionar el array en dos subarrays: uno con elementos menores al pivote y otro con elementos mayores al pivote. Luego, se ordenan recursivamente los subarrays.

#### Funcionamiento de Quicksort

1. Seleccionar un **pivote** (puede ser el primer elemento, el último, o el medio del array).
2. Reordenar los elementos del array para que todos los elementos menores al pivote estén antes y los elementos mayores al pivote estén después.
3. Aplicar recursivamente el mismo proceso a los subarrays izquierdo y derecho generados por el pivote.

#### Implementación de Quicksort

```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)
```

#### Complejidad Temporal

- **Mejor caso**: **O(n log n)** (cuando el pivote divide el array en partes iguales).
- **Peor caso**: **O(n^2)** (cuando el pivote elegido no divide bien el array, como en un array ya ordenado).
- **Caso promedio**: **O(n log n)**.

### Mergesort

El **Mergesort** es otro algoritmo de ordenamiento basado en la técnica de **divide y vencerás**. A diferencia de Quicksort, Mergesort divide el array en dos mitades iguales, las ordena recursivamente y luego las combina (merge) de manera ordenada.

#### Funcionamiento de Mergesort

1. Dividir el array en dos mitades.
2. Ordenar recursivamente cada mitad.
3. Combinar las dos mitades ordenadas en un array ordenado.

#### Implementación de Mergesort

```python
def mergesort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = mergesort(arr[:mid])
    right = mergesort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

#### Complejidad Temporal

- **Mejor caso**: **O(n log n)**.
- **Peor caso**: **O(n log n)**.
- **Caso promedio**: **O(n log n)**.

El Mergesort tiene una complejidad temporal de **O(n log n)** en todos los casos, ya que siempre divide el array en dos mitades y luego las fusiona de manera ordenada.

### Comparación de Quicksort y Mergesort

| Algoritmo  | Complejidad Mejor Caso | Complejidad Peor Caso | Complejidad Promedio | Estabilidad  | Uso de Memoria |
|------------|------------------------|-----------------------|----------------------|--------------|----------------|
| **Quicksort** | O(n log n)             | O(n^2)                | O(n log n)           | No           | O(log n)       |
| **Mergesort** | O(n log n)             | O(n log n)            | O(n log n)           | Sí           | O(n)           |

### Resumen

1. **Quicksort** es rápido en la mayoría de los casos (O(n log n)) y es preferido cuando el rendimiento es crítico y el array no está ordenado previamente.
2. **Mergesort** tiene una complejidad de O(n log n) en todos los casos, es estable (mantiene el orden relativo de elementos iguales) y utiliza más memoria debido a la necesidad de crear arrays adicionales.

### Conclusión

Tanto **Quicksort** como **Mergesort** son algoritmos muy eficientes con complejidad **O(n log n)** en el caso promedio. La elección entre uno u otro depende del contexto:
- Si la estabilidad es importante, **Mergesort** es la opción adecuada.
- Si se necesita un algoritmo más rápido en promedio y se puede tolerar un peor caso **O(n^2)** ocasional, **Quicksort** es una excelente opción.
