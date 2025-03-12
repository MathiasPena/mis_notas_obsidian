
### ¿Qué son el Stack y el Heap?

En la programación, la memoria se organiza en dos áreas principales: **Stack** y **Heap**. Ambos tienen propósitos distintos en la gestión de la memoria y el almacenamiento de datos.

#### 1. Stack (Pila)

- **Definición**: El **Stack** es una estructura de datos en la memoria que se utiliza para almacenar las **variables locales** y las **funciones activas** en un programa. Funciona como una pila, en la que los datos se apilan y desapilan en orden **Last In, First Out (LIFO)**.
  
- **Características**:
  - **Rápido y eficiente**: Acceder a la memoria en el Stack es más rápido porque la memoria se gestiona de forma automática, con cada función apilando y desapilando su propia memoria.
  - **Memoria limitada**: La memoria disponible en el Stack es más limitada y se libera automáticamente cuando una función termina de ejecutarse.
  - **Almacenamiento de datos**: Solo almacena referencias a objetos y valores primitivos (números, cadenas, etc.). Las variables locales son gestionadas en el Stack.
  - **Ciclo de vida**: La memoria del Stack es temporal y se gestiona automáticamente cuando las funciones terminan su ejecución.

#### 2. Heap (Montículo)

- **Definición**: El **Heap** es una región de la memoria donde se almacenan los **objetos dinámicos** que requieren una gestión más flexible en cuanto a su tamaño y ciclo de vida.
  
- **Características**:
  - **Más flexible**: Los datos almacenados en el Heap pueden ser más grandes y no están limitados por el tamaño de la pila.
  - **Acceso más lento**: La gestión de memoria en el Heap es más compleja, lo que resulta en un acceso más lento en comparación con el Stack.
  - **Almacenamiento de objetos**: Los objetos que se crean dinámicamente, como instancias de clases o estructuras de datos más complejas (listas, diccionarios, etc.), se almacenan en el Heap.
  - **Ciclo de vida**: Los objetos en el Heap persisten hasta que se liberen explícitamente o cuando ya no tienen referencias, momento en el cual el recolector de basura de Python los elimina.

### Diferencias clave entre Stack y Heap

| Característica         | Stack                         | Heap                          |
|------------------------|-------------------------------|-------------------------------|
| **Ubicación**          | Memoria de acceso rápido      | Memoria de acceso más lento   |
| **Gestión**            | Automática (al entrar/salir de funciones) | Manual, con recolector de basura |
| **Tamaño**             | Limitado y pequeño            | Más grande y flexible         |
| **Ciclo de vida**      | Temporal (hasta que la función termine) | Persistente hasta que se libera la memoria |
| **Almacenamiento**     | Variables locales, funciones  | Objetos dinámicos, estructuras complejas |
| **Acceso**             | Muy rápido                    | Más lento debido a la fragmentación |

### Cómo se asigna la memoria en Python

En Python, la gestión de la memoria se combina con el uso del **Stack** y el **Heap** de la siguiente manera:

- **Variables locales** (por ejemplo, enteros o cadenas simples) se almacenan en el Stack.
- **Objetos complejos** como listas, diccionarios y objetos de clases se almacenan en el Heap.

Cuando creas una instancia de un objeto en Python:

```python
my_list = [1, 2, 3, 4]
```

- La **referencia** a `my_list` se almacena en el Stack.
- El **contenido de la lista** (es decir, los valores `[1, 2, 3, 4]`) se almacena en el Heap.

### Ciclo de vida de los objetos en el Stack y el Heap

1. **Stack**:
   - Cuando una función es llamada, las variables locales se apilan.
   - Cuando la función termina, esas variables se desapilan automáticamente.
   - Las variables del Stack son de **vida corta**.

2. **Heap**:
   - Los objetos que se crean dinámicamente permanecen en el Heap hasta que no hay más referencias a ellos.
   - **Python** utiliza un recolector de basura (garbage collector) para liberar la memoria de objetos en el Heap que ya no están en uso.

### Impacto del Stack y Heap en el rendimiento

- **Stack**:
  - Es rápido debido a su gestión automática.
  - No genera mucha sobrecarga, pero tiene un límite en cuanto a la cantidad de memoria que puede manejar (generalmente, las variables locales tienen que ser relativamente pequeñas).

- **Heap**:
  - Su acceso es más lento debido a la necesidad de gestionar la memoria de manera más compleja.
  - Los objetos que se almacenan en el Heap pueden durar más tiempo en la memoria, lo que puede llevar a **fragmentación de memoria** si no se gestionan correctamente.

### Ejemplo práctico

```python
def ejemplo_stack_heap():
    # Stack: variable local
    num = 42

    # Heap: objeto dinámico
    my_list = [1, 2, 3, 4]

    print(num)
    print(my_list)

ejemplo_stack_heap()
```

- `num` se almacena en el Stack.
- `my_list` se almacena en el Heap (y se mantiene allí hasta que el recolector de basura de Python lo elimine).

### Conclusión

El **Stack** y el **Heap** son dos áreas importantes en la gestión de memoria. El Stack se utiliza para datos temporales y de acceso rápido, mientras que el Heap maneja los objetos dinámicos y más grandes. En Python, la interacción entre ambos es gestionada automáticamente, con el Stack manejando las variables locales y el Heap almacenando los objetos más complejos. Conocer cómo funcionan y cómo afectan el rendimiento es crucial para escribir código eficiente y comprender cómo se gestiona la memoria, especialmente en aplicaciones de gran escala como las que se pueden encontrar en **Data Engineering**.
