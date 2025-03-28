El Heap es la memoria donde se almacenan los objetos en tiempo de ejecución.
    Características clave:
    - Es compartido por todos los hilos de la JVM.
    - Contiene objetos y sus datos asociados.
    - Está gestionado por el Garbage Collector.
    - Se divide en:
      1. **Young Generation** (Eden, Survivor 0, Survivor 1)
      2. **Old Generation** (Tenured)
      3. **Metaspace** (para metadatos de clases)

```java

class HeapExample {
    public static void main(String[] args) {
        // Estos objetos se almacenan en el Heap
        Person p1 = new Person("Juan");
        Person p2 = new Person("Ana");

        // Se imprimen los nombres desde el Heap
        System.out.println(p1.getName());
        System.out.println(p2.getName());
    }
}

class Person {
    private String name;

    public Person(String name) {
        this.name = name;  // El String se almacena en el Heap
    }

    public String getName() {
        return name;
    }
}

/*
    **Explicación**
    - `p1` y `p2` son referencias en la Stack, pero los objetos están en el Heap.
    - El `name` de cada objeto también está en el Heap.
*/


// ===================================
// 2. EJEMPLO DE YOUNG GENERATION
// ===================================

class YoungGenExample {
    public static void main(String[] args) {
        for (int i = 0; i < 10_000; i++) {
            new Person("Persona " + i); // Se crean objetos en el Heap (Eden)
        }

        // Sugerimos al Garbage Collector que limpie memoria
        System.gc();
        System.out.println("Fin del programa.");
    }
}

/*
    **Explicación**
    - Los objetos nuevos se crean en **Eden** (Young Generation).
    - Si sobreviven varias recolecciones de basura, pasan a **Survivor 0** y luego a **Survivor 1**.
    - Si siguen vivos, se mueven a la **Old Generation**.
*/


// ===================================
// 3. EJEMPLO DE OLD GENERATION (TENURED)
// ===================================

class OldGenExample {
    public static void main(String[] args) {
        // Creamos un objeto grande que se mantendrá en memoria
        int[] bigArray = new int[10_000_000]; // Se almacena en el Heap (Old Gen)

        // Usamos los datos para evitar optimización del compilador
        for (int i = 0; i < bigArray.length; i++) {
            bigArray[i] = i;
        }

        System.out.println("Array grande creado y almacenado en el Heap.");
    }
}

/*
    **Explicación**
    - Un objeto grande como `bigArray` se almacena directamente en la **Old Generation**.
    - Los objetos en Old Gen viven más tiempo y son recolectados con GC de pausas largas (Full GC).
*/


// ===================================
// 4. EJEMPLO DE GARBAGE COLLECTOR EN HEAP
// ===================================

class GarbageCollectorHeapExample {
    public static void main(String[] args) {
        Person p1 = new Person("Carlos");
        Person p2 = new Person("Lucía");

        // Eliminamos referencias
        p1 = null;
        p2 = null;

        // Sugerimos al Garbage Collector que limpie memoria
        System.gc();

        System.out.println("Se sugirió al Garbage Collector que limpie.");
    }

    // Método especial que se ejecuta antes de eliminar un objeto
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Objeto eliminado por el Garbage Collector.");
    }
}

/*
    **Explicación**
    - Cuando `p1` y `p2` quedan en `null`, sus objetos en el Heap quedan inaccesibles.
    - `System.gc()` sugiere ejecutar el Garbage Collector (aunque no es inmediato).
    - `finalize()` se ejecuta antes de que el objeto sea eliminado.
*/


// ===================================
// 5. DEMOSTRACIÓN DE MEMORY LEAK EN HEAP
// ===================================

import java.util.ArrayList;
import java.util.List;

class MemoryLeakExample {
    private static final List<byte[]> memoryLeakList = new ArrayList<>();

    public static void main(String[] args) {
        while (true) {
            memoryLeakList.add(new byte[1_000_000]); // Se crean objetos grandes en el Heap
            System.out.println("Memoria utilizada: " + memoryLeakList.size() + " MB");
        }
    }
}

/*
    **Explicación**
    - Este código crea un Memory Leak llenando el Heap con objetos sin ser eliminados.
    - Provoca un `OutOfMemoryError: Java heap space`.
*/


// ===================================
// 6. AJUSTES DE HEAP EN JVM
// ===================================

/*
    Se pueden ajustar los tamaños de Heap con flags de JVM:

    -Xms<size>  -> Tamaño inicial del Heap.
    -Xmx<size>  -> Tamaño máximo del Heap.
    -XX:NewRatio=<n>  -> Relación entre Old Gen y Young Gen.
    -XX:SurvivorRatio=<n>  -> Relación entre Eden y Survivor Spaces.
    -XX:+UseG1GC  -> Activa el Garbage Collector G1GC.

    Ejemplo de ejecución:
    java -Xms128M -Xmx512M -XX:+UseG1GC HeapExample
*/


// ===================================
// CONCLUSIÓN
// ===================================

/*
    RESUMEN DEL HEAP EN JAVA:
    -------------------------
    - El Heap es el área de memoria donde se almacenan los objetos en tiempo de ejecución.
    - Se divide en **Young Generation**, **Old Generation** y **Metaspace**.
    - **Young Generation** maneja objetos nuevos y se subdivide en Eden y Survivor Spaces.
    - **Old Generation** almacena objetos de larga duración.
    - **Garbage Collector** libera memoria eliminando objetos sin referencia.
    - El mal uso del Heap puede generar **OutOfMemoryError** o Memory Leaks.

    ¡Con esto ya cubrimos TODO sobre el Heap en Java!
*/

```