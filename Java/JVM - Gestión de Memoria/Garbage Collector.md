 - Java maneja la memoria automáticamente con el Garbage Collector (GC).
    - El GC elimina objetos no referenciados para liberar memoria.
    - Tipos de referencias en Java:
      1. Referencias fuertes (Strong References)
      2. Referencias débiles (Weak References)
      3. Referencias suaves (Soft References)
      4. Referencias fantasmas (Phantom References) (más avanzadas)

    - Para sugerir la ejecución del GC: System.gc() (no garantiza ejecución).
    - Se pueden usar herramientas como `jvisualvm` para monitorear el GC.

```java
// ===================================
// 1. REFERENCIAS FUERTES (STRONG REFERENCES)
// ===================================

public class StrongReferenceExample {
    public static void main(String[] args) {
        // Referencia fuerte: el objeto no será eliminado por el GC mientras haya una referencia a él.
        Object strongRef = new Object();
        System.out.println("Objeto con referencia fuerte: " + strongRef);

        // Si lo ponemos en null, el GC lo eliminará en algún momento.
        strongRef = null;

        // Sugerimos al GC que libere memoria (pero no es obligatorio)
        System.gc();
    }
}

/*
    **Explicación**
    - Mientras `strongRef` apunte al objeto, este no será eliminado por el GC.
    - Al hacer `strongRef = null`, el objeto queda elegible para ser recolectado.
    - `System.gc()` sugiere la recolección, pero la JVM decide cuándo ejecutarla.
*/


// ===================================
// 2. REFERENCIAS DÉBILES (WEAK REFERENCES)
// ===================================

import java.lang.ref.WeakReference;

public class WeakReferenceExample {
    public static void main(String[] args) {
        Object strongObject = new Object();
        WeakReference<Object> weakRef = new WeakReference<>(strongObject);

        System.out.println("Objeto antes de GC: " + weakRef.get());

        // Eliminamos la referencia fuerte
        strongObject = null;

        // Sugerimos al GC que limpie
        System.gc();

        // Esperamos un poco para ver si el GC elimina el objeto
        try { Thread.sleep(1000); } catch (InterruptedException e) {}

        System.out.println("Objeto después del GC: " + weakRef.get()); // Probablemente sea null
    }
}

/*
    **Explicación**
    - `WeakReference<Object> weakRef` mantiene una referencia débil a un objeto.
    - Cuando no hay referencias fuertes al objeto, el GC lo elimina.
    - `weakRef.get()` devolverá `null` si el objeto ha sido recolectado.
    - Se usa en cachés donde no queremos que los objetos bloqueen la memoria innecesariamente.
*/


// ===================================
// 3. REFERENCIAS SUAVES (SOFT REFERENCES)
// ===================================

import java.lang.ref.SoftReference;

public class SoftReferenceExample {
    public static void main(String[] args) {
        Object strongObject = new Object();
        SoftReference<Object> softRef = new SoftReference<>(strongObject);

        System.out.println("Objeto antes de GC: " + softRef.get());

        // Eliminamos la referencia fuerte
        strongObject = null;

        // Sugerimos al GC que limpie
        System.gc();

        // Esperamos un poco para ver si el GC elimina el objeto
        try { Thread.sleep(1000); } catch (InterruptedException e) {}

        System.out.println("Objeto después del GC: " + softRef.get()); // Puede seguir existiendo
    }
}

/*
    **Explicación**
    - `SoftReference<Object> softRef` mantiene una referencia blanda al objeto.
    - A diferencia de `WeakReference`, el GC solo eliminará objetos con referencias suaves cuando haya presión de memoria.
    - Se usa para cachés que pueden mantenerse hasta que la memoria se agote.
*/


// ===================================
// 4. REFERENCIAS FANTASMAS (PHANTOM REFERENCES)
// ===================================

import java.lang.ref.PhantomReference;
import java.lang.ref.ReferenceQueue;

public class PhantomReferenceExample {
    public static void main(String[] args) {
        Object strongObject = new Object();
        ReferenceQueue<Object> refQueue = new ReferenceQueue<>();
        PhantomReference<Object> phantomRef = new PhantomReference<>(strongObject, refQueue);

        System.out.println("Objeto antes del GC: " + phantomRef.get()); // Siempre será null

        // Eliminamos la referencia fuerte
        strongObject = null;

        // Sugerimos al GC que limpie
        System.gc();

        // Esperamos a que el objeto sea eliminado y referenciado en la queue
        try { Thread.sleep(1000); } catch (InterruptedException e) {}

        System.out.println("¿Objeto en la queue?: " + (refQueue.poll() != null));
    }
}

/*
    **Explicación**
    - `PhantomReference<Object> phantomRef` no permite acceder directamente al objeto.
    - Se usa con `ReferenceQueue` para detectar cuándo el GC ha eliminado el objeto.
    - Se usa en manejo avanzado de memoria, como liberar recursos nativos.
*/


// ===================================
// 5. FORZAR LA RECOLECCIÓN DE BASURA
// ===================================

public class ForceGarbageCollection {
    public static void main(String[] args) {
        Object obj = new Object();
        System.out.println("Objeto creado: " + obj);

        obj = null; // Hacemos el objeto elegible para el GC

        System.gc(); // Sugerimos ejecutar el Garbage Collector

        // Esperamos un poco
        try { Thread.sleep(1000); } catch (InterruptedException e) {}

        System.out.println("Fin del programa.");
    }
}

/*
    **Explicación**
    - `System.gc()` sugiere ejecutar el GC, pero la JVM decide si hacerlo o no.
    - El objeto queda elegible para ser recolectado al asignarlo a `null`.
*/


// ===================================
// 6. FINALIZADORES Y USO DE finalize() (OBSOLETO EN JAVA 9+)
// ===================================

class FinalizableObject {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Objeto recolectado por el Garbage Collector.");
    }
}

public class FinalizeExample {
    public static void main(String[] args) {
        FinalizableObject obj = new FinalizableObject();
        obj = null; // Hacemos el objeto elegible para el GC

        System.gc(); // Sugerimos ejecutar el GC

        // Esperamos un poco
        try { Thread.sleep(1000); } catch (InterruptedException e) {}

        System.out.println("Fin del programa.");
    }
}

/*
    **Explicación**
    - `finalize()` es llamado antes de que el GC elimine un objeto.
    - No es confiable porque puede no ejecutarse antes de que la JVM termine.
    - Se eliminó en Java 9 en favor de `try-with-resources` y `PhantomReferences`.
*/


// ===================================
// 7. MONITOREAR EL GARBAGE COLLECTOR
// ===================================

import java.lang.management.ManagementFactory;
import java.lang.management.GarbageCollectorMXBean;
import java.util.List;

public class MonitorGarbageCollector {
    public static void main(String[] args) {
        List<GarbageCollectorMXBean> gcBeans = ManagementFactory.getGarbageCollectorMXBeans();

        for (GarbageCollectorMXBean gcBean : gcBeans) {
            System.out.println("Garbage Collector: " + gcBean.getName());
            System.out.println("Total ejecuciones: " + gcBean.getCollectionCount());
            System.out.println("Tiempo total (ms): " + gcBean.getCollectionTime());
            System.out.println("------------------------------");
        }
    }
}

/*
    **Explicación**
    - `ManagementFactory.getGarbageCollectorMXBeans()` obtiene los GC disponibles en la JVM.
    - Muestra la cantidad de ejecuciones y el tiempo total usado por el GC.
*/


// ===================================
// 8. CONCLUSIÓN
// ===================================

/*
    RESUMEN SOBRE GARBAGE COLLECTOR:
    --------------------------------
    - Java usa el GC para eliminar objetos no referenciados y liberar memoria.
    - Existen 4 tipos de referencias: fuerte, débil, suave y fantasma.
    - `System.gc()` sugiere ejecutar el GC, pero no lo garantiza.
    - `WeakReference` y `SoftReference` ayudan a manejar cachés y evitar memory leaks.
    - `PhantomReference` se usa para detectar la recolección de un objeto sin acceder a él.
    - `finalize()` está obsoleto desde Java 9.
    - Se pueden monitorear los GC con `GarbageCollectorMXBean`.
```