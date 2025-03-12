# Python para Data Engineering - Teoría Interna y Conceptos Avanzados

## 3. Garbage Collector y gc module

### ¿Qué es el Garbage Collector en Python?

El **Garbage Collector (GC)** en Python es un mecanismo automático que gestiona la memoria eliminando los objetos que ya no son accesibles o que no tienen referencias activas. El objetivo es liberar memoria que ya no se está utilizando, evitando así **fugas de memoria** y garantizando que los recursos sean gestionados de manera eficiente.

En **CPython** (la implementación más común de Python), el **Garbage Collector** se basa en dos técnicas principales:

1. **Contador de referencias**: 
   - Cada objeto en Python mantiene un contador de cuántas referencias apuntan a él. Cuando el contador llega a cero (es decir, no hay más referencias al objeto), el objeto se elimina de la memoria.
   
2. **Recolección de ciclos de referencia**: 
   - Aunque el contador de referencias es eficaz para la mayoría de los casos, no puede gestionar correctamente los ciclos de referencia (cuando dos o más objetos se referencian mutuamente). En estos casos, el Garbage Collector de Python puede identificar estos ciclos y liberarlos de forma eficiente.

### ¿Cómo funciona el Garbage Collector?

1. **Contador de referencias**:
   - Cada vez que se crea una nueva referencia a un objeto, su contador de referencias se incrementa. Si una referencia a un objeto se elimina o se reasigna, el contador disminuye.
   - Cuando el contador de referencias llega a cero, el objeto es destruido automáticamente.

2. **Recolección de ciclos de referencia**:
   - El contador de referencias no puede detectar los ciclos de referencia, es decir, cuando dos o más objetos se referencian entre sí, creando un ciclo. Para estos casos, el GC utiliza un algoritmo de recolección de ciclos para detectar y eliminar estos ciclos de referencia.

   **Ejemplo de ciclo de referencia**:

   ```python
   class A:
       def __init__(self):
           self.ref = None

   obj1 = A()
   obj2 = A()

   obj1.ref = obj2
   obj2.ref = obj1
   ```

   En este caso, `obj1` y `obj2` se refieren entre sí, formando un ciclo. Si no se manejara adecuadamente, estos objetos nunca serían liberados debido a que sus contadores de referencia nunca llegarían a cero.

### ¿Qué es el módulo `gc`?

El módulo **`gc`** es una interfaz en Python que permite interactuar y controlar el **Garbage Collector**. A través de este módulo, puedes realizar tareas como:

- **Forzar la recolección de basura**.
- **Obtener estadísticas sobre el GC**.
- **Deshabilitar temporalmente el GC**.
- **Identificar ciclos de referencia**.

### Funciones más comunes del módulo `gc`

1. **gc.collect()**: Forzar la recolección de basura.
   - Puedes invocar esta función para forzar la ejecución del Garbage Collector y eliminar objetos no referenciados. Este proceso puede ser útil en programas con un uso intensivo de memoria.
   
   ```python
   import gc
   gc.collect()
   ```

2. **gc.get_count()**: Obtener estadísticas sobre el GC.
   - Devuelve el número de objetos que el GC ha asignado a diferentes generaciones.
   
   ```python
   import gc
   print(gc.get_count())  # Devuelve el número de objetos en cada generación
   ```

3. **gc.get_objects()**: Obtener una lista de todos los objetos gestionados por el GC.
   - Permite inspeccionar todos los objetos actuales que el Garbage Collector está gestionando.

   ```python
   import gc
   print(gc.get_objects())  # Devuelve una lista de objetos
   ```

4. **gc.set_debug(flags)**: Configurar el modo de depuración del GC.
   - Permite configurar el GC para mostrar información de depuración detallada sobre la recolección de basura.

   ```python
   import gc
   gc.set_debug(gc.DEBUG_LEAK)
   ```

### Generaciones de objetos y el ciclo de recolección

El Garbage Collector de Python utiliza un sistema basado en **generaciones** para optimizar la recolección de basura:

1. **Generación 0**: Es la generación más joven, donde se colocan los objetos recién creados. Los objetos en esta generación son recolectados con mayor frecuencia.
2. **Generación 1**: Si un objeto sobrevive a una recolección de la Generación 0, pasa a la Generación 1. Esta recolección ocurre con menos frecuencia.
3. **Generación 2**: Es la generación más antigua. Los objetos que sobreviven a la recolección de la Generación 1 se mueven aquí. La recolección de la Generación 2 es menos frecuente.

El Garbage Collector realiza la recolección más frecuentemente en la **Generación 0**, ya que muchos objetos en esta generación tienden a ser desechados rápidamente. Las generaciones 1 y 2 se recolectan con menos frecuencia, ya que los objetos que sobreviven más tiempo son más difíciles de eliminar.

### Ciclos de referencia y cómo el GC los maneja

El GC es capaz de detectar **ciclos de referencia** y liberarlos, lo que le permite manejar mejor los objetos interdependientes que de otro modo no se liberarían debido a los contadores de referencias circulares. Estos ciclos suelen ser creados cuando dos o más objetos se refieren entre sí, impidiendo que su contador de referencias llegue a cero.

### Ejemplo de uso del módulo `gc`

```python
import gc

class Object:
    def __init__(self):
        self.data = [1, 2, 3]

    def __del__(self):
        print("Eliminando objeto")

# Crear objetos
obj1 = Object()
obj2 = Object()

# Crear ciclo de referencia
obj1.ref = obj2
obj2.ref = obj1

# Forzar recolección de basura
gc.collect()

# Comprobar estadísticas del GC
print(gc.get_count())
```

### Deshabilitar el Garbage Collector

En algunas situaciones, es posible que desees desactivar temporalmente el GC para optimizar el rendimiento, especialmente en tareas donde se sabe que la memoria no se gestionará de manera intensiva durante un largo período de tiempo.

```python
import gc

# Desactivar el GC
gc.disable()

# Ejecutar el código sin la intervención del GC

# Volver a habilitar el GC
gc.enable()
```

### Conclusión

El **Garbage Collector (GC)** en Python es un mecanismo crucial para la gestión eficiente de la memoria, automatizando la eliminación de objetos no referenciados. Aunque el GC está diseñado para manejar la memoria automáticamente, el módulo **`gc`** permite un control más preciso y la posibilidad de intervenir en la recolección de basura, especialmente en situaciones que requieren optimización. Comprender cómo funciona el GC y cómo interactuar con él es esencial para desarrollar aplicaciones eficientes, especialmente en entornos con uso intensivo de memoria.
