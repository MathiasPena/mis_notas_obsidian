Metaspace es la memoria donde la JVM almacena metadatos de clases y estructuras internas.
    - Introducido en Java 8 (sustituyó Permanent Generation - PermGen).
    - Gestionado dinámicamente por la JVM.
    - No tiene un límite fijo por defecto, crece según la necesidad.
    - Se puede controlar su tamaño con los flags de la JVM.

En Metaspace se almacenan:
    - Definiciones de clases (metadata de clases cargadas).
    - Métodos y estructuras internas de las clases.
    - Información de la JVM sobre los tipos de datos.

    Los objetos NO están en Metaspace, sino en el Heap.

```java
// ===================================
// 2. EJEMPLO DE CARGA DINÁMICA DE CLASES EN METASPACE
// ===================================

import java.lang.reflect.Proxy;
import java.util.ArrayList;
import java.util.List;

class MetaspaceExample {
    public static void main(String[] args) {
        List<ClassLoader> classLoaders = new ArrayList<>();

        try {
            while (true) {
                // Crear un nuevo ClassLoader que carga clases dinámicamente
                ClassLoader classLoader = new CustomClassLoader();
                classLoaders.add(classLoader);

                // Cargar una clase ficticia en memoria
                Class<?> dynamicClass = classLoader.loadClass("MiClaseDinamica");
                System.out.println("Clase cargada: " + dynamicClass.getName());
            }
        } catch (OutOfMemoryError e) {
            System.err.println("¡Se agotó el espacio en Metaspace!");
        }
    }
}

class CustomClassLoader extends ClassLoader {
    @Override
    public Class<?> loadClass(String name) throws ClassNotFoundException {
        return Proxy.getProxyClass(getClass().getClassLoader(), Runnable.class);
    }
}

/*
    **Explicación**
    - Creamos una lista de `ClassLoader` para cargar clases dinámicamente.
    - En un bucle infinito, seguimos cargando nuevas clases en Metaspace.
    - Eventualmente, se lanza un `OutOfMemoryError` cuando la JVM no puede seguir reservando memoria.
*/


// ===================================
// 3. CONFIGURAR EL TAMAÑO DE METASPACE EN JVM
// ===================================

/*
    Se pueden usar flags de la JVM para controlar Metaspace:

    -XX:MetaspaceSize=128M        -> Tamaño inicial de Metaspace.
    -XX:MaxMetaspaceSize=256M     -> Tamaño máximo de Metaspace.
    -XX:+UseGCOverheadLimit       -> Habilita la recolección de basura cuando Metaspace crece mucho.

    Ejemplo de ejecución:
    java -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=256M MetaspaceExample
*/


// ===================================
// 4. ¿CÓMO SE LIBERA MEMORIA EN METASPACE?
// ===================================

/*
    - La JVM usa el Garbage Collector para liberar Metaspace cuando ya no se necesitan clases cargadas.
    - Si una aplicación usa muchos ClassLoaders dinámicos (como frameworks), Metaspace puede crecer demasiado.
    - Si Metaspace crece sin control, puede generar un OutOfMemoryError.
*/


// ===================================
// 5. EJEMPLO DE GESTIÓN DE METASPACE CON GC
// ===================================

class GCMetaspaceExample {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            CustomClassLoader loader = new CustomClassLoader();
            try {
                Class<?> dynamicClass = loader.loadClass("MiClaseDinamica");
                System.out.println("Clase cargada: " + dynamicClass.getName());
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            }

            // Forzamos la recolección de basura para intentar liberar Metaspace
            System.gc();
        }
    }
}

/*
    **Explicación**
    - Creamos y cargamos clases dinámicamente.
    - Llamamos a `System.gc()` para intentar liberar memoria de Metaspace.
    - Si un `ClassLoader` ya no tiene referencias activas, la JVM puede liberar Metaspace.
*/


// ===================================
// CONCLUSIÓN
// ===================================

/*
    RESUMEN DE METASPACE EN JAVA:
    -----------------------------
    - Es la memoria donde la JVM almacena metadatos de clases y estructuras internas.
    - Reemplazó a PermGen en Java 8 y es más eficiente.
    - No tiene un límite fijo por defecto, pero puede configurarse.
    - Si se llena, lanza un `OutOfMemoryError`.
    - Puede crecer mucho si la aplicación carga muchas clases dinámicamente.
    - El Garbage Collector puede liberar Metaspace si los ClassLoaders dejan de estar referenciados.
```