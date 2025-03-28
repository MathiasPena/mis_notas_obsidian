- Un ClassLoader es un componente de la JVM responsable de cargar clases en tiempo de ejecución.
    - Java usa un sistema jerárquico de ClassLoaders.
    - Existen tres tipos principales de ClassLoaders:
      1. Bootstrap ClassLoader
      2. Extension ClassLoader (o Platform ClassLoader en Java 9+)
      3. Application ClassLoader (o System ClassLoader)

```java
// ===================================
// 1. HIERARQUÍA DE CLASSLOADERS
// ===================================

public class ClassLoaderHierarchy {
    public static void main(String[] args) {
        // Obtener el ClassLoader de la clase actual
        ClassLoader classLoader = ClassLoaderHierarchy.class.getClassLoader();
        System.out.println("ClassLoader actual: " + classLoader);

        // Obtener el ClassLoader padre (Platform ClassLoader en Java 9+)
        ClassLoader parentClassLoader = classLoader.getParent();
        System.out.println("Parent ClassLoader: " + parentClassLoader);

        // Obtener el ClassLoader superior (Bootstrap ClassLoader)
        ClassLoader bootstrapClassLoader = parentClassLoader.getParent();
        System.out.println("Bootstrap ClassLoader: " + bootstrapClassLoader); // Debería ser null
    }
}

/*
    **Salida esperada**
    ------------------
    ClassLoader actual: jdk.internal.loader.ClassLoaders$AppClassLoader@...
    Parent ClassLoader: jdk.internal.loader.ClassLoaders$PlatformClassLoader@...
    Bootstrap ClassLoader: null

    **Explicación**
    - `AppClassLoader` carga las clases del classpath.
    - `PlatformClassLoader` carga clases del JDK (Java 9+).
    - `Bootstrap ClassLoader` carga clases del núcleo de Java (rt.jar, ahora en el módulo java.base).
*/


// ===================================
// 2. CARGAR UNA CLASE MANUALMENTE CON Class.forName()
// ===================================

public class LoadClassExample {
    public static void main(String[] args) {
        try {
            // Cargar una clase usando el ClassLoader del sistema
            Class<?> loadedClass = Class.forName("java.util.ArrayList");
            System.out.println("Clase cargada: " + loadedClass.getName());
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

/*
    **Explicación**
    - `Class.forName("java.util.ArrayList")` busca y carga la clase `ArrayList`.
    - Devuelve un objeto `Class<?>` con información de la clase.
*/


// ===================================
// 3. CREAR UN CLASSLOADER PERSONALIZADO
// ===================================

import java.io.*;

class MyClassLoader extends ClassLoader {
    @Override
    public Class<?> loadClass(String name) throws ClassNotFoundException {
        if (!name.startsWith("com.miproyecto")) {
            // Delega la carga de clases al ClassLoader padre (sistema)
            return super.loadClass(name);
        }

        try {
            String filePath = name.replace('.', '/') + ".class";
            InputStream input = getClass().getClassLoader().getResourceAsStream(filePath);
            if (input == null) {
                throw new ClassNotFoundException(name);
            }

            byte[] classBytes = input.readAllBytes();
            return defineClass(name, classBytes, 0, classBytes.length);
        } catch (IOException e) {
            throw new ClassNotFoundException(name, e);
        }
    }
}

public class CustomClassLoaderExample {
    public static void main(String[] args) {
        try {
            MyClassLoader myLoader = new MyClassLoader();
            Class<?> myClass = myLoader.loadClass("com.miproyecto.MiClase");
            System.out.println("Clase cargada con MyClassLoader: " + myClass.getName());
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

/*
    **Explicación**
    - `MyClassLoader` extiende `ClassLoader` para cargar clases de un paquete específico.
    - Reemplazamos el método `loadClass()` para cargar clases desde un archivo `.class`.
    - Si la clase no está en `com.miproyecto`, delega la carga al ClassLoader padre.
*/


// ===================================
// 4. OBTENER EL CLASSLOADER DE UNA CLASE
// ===================================

public class GetClassLoaderExample {
    public static void main(String[] args) {
        // Obtener el ClassLoader de una clase específica
        ClassLoader classLoader = String.class.getClassLoader();
        System.out.println("ClassLoader de String: " + classLoader); // Debe ser null porque la carga el Bootstrap ClassLoader

        classLoader = GetClassLoaderExample.class.getClassLoader();
        System.out.println("ClassLoader de esta clase: " + classLoader);
    }
}

/*
    **Explicación**
    - `String.class.getClassLoader()` devuelve `null` porque `String` es cargado por el Bootstrap ClassLoader.
    - `GetClassLoaderExample.class.getClassLoader()` devuelve el `Application ClassLoader`.
*/


// ===================================
// 5. VER TODAS LAS CLASES CARGADAS EN UN CLASSLOADER
// ===================================

import java.lang.management.ManagementFactory;
import java.lang.management.ClassLoadingMXBean;

public class LoadedClassesExample {
    public static void main(String[] args) {
        // Obtener información sobre las clases cargadas en la JVM
        ClassLoadingMXBean classLoadingMXBean = ManagementFactory.getClassLoadingMXBean();

        System.out.println("Clases actualmente cargadas: " + classLoadingMXBean.getLoadedClassCount());
        System.out.println("Total de clases cargadas desde el inicio: " + classLoadingMXBean.getTotalLoadedClassCount());
        System.out.println("Total de clases descargadas: " + classLoadingMXBean.getUnloadedClassCount());
    }
}

/*
    **Explicación**
    - `getLoadedClassCount()` muestra el número actual de clases cargadas.
    - `getTotalLoadedClassCount()` muestra el total de clases cargadas desde que comenzó la JVM.
    - `getUnloadedClassCount()` muestra las clases eliminadas de la memoria.
*/


// ===================================
// 6. CONCLUSIÓN
// ===================================

/*
    RESUMEN DE CLASSLOADER EN JAVA:
    -------------------------------
    - Los ClassLoaders cargan clases en tiempo de ejecución.
    - Siguen una jerarquía: Bootstrap, Platform y Application ClassLoader.
    - `Class.forName()` permite cargar clases en tiempo de ejecución.
    - Se pueden crear ClassLoaders personalizados para cargar clases de fuentes externas.
    - `ClassLoader.getResourceAsStream()` permite leer archivos dentro del classpath.
    - `ManagementFactory.getClassLoadingMXBean()` permite obtener estadísticas sobre clases cargadas.
```