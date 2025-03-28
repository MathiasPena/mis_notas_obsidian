La JVM divide la memoria en diferentes regiones para gestionar los objetos:
 * 1. Young Generation (Eden + Survivor Spaces)
 * 2. Old Generation (Tenured)
 * 3. Permanent Generation (hasta Java 7) / Metaspace (Java 8+)

```java
public class MemoryLifecycleDemo {
    public static void main(String[] args) {
        simulateYoungGeneration();
        simulateOldGeneration();
    }

    // Simula la Young Generation
    private static void simulateYoungGeneration() {
        System.out.println("Creando objetos en Young Generation (Eden)...");
        for (int i = 0; i < 10_000; i++) {
            byte[] temp = new byte[1024]; // 1KB por objeto
        }
        System.out.println("Algunos objetos sobreviven y pasan a Survivor Spaces.");
    }

    // Simula la Old Generation
    private static void simulateOldGeneration() {
        System.out.println("Creando objetos de larga vida en Old Generation...");
        byte[][] oldObjects = new byte[100][1024 * 1024]; // 100MB en total
        for (int i = 0; i < oldObjects.length; i++) {
            oldObjects[i] = new byte[1024 * 1024]; // 1MB por objeto
        }
        System.out.println("Los objetos persistentes se mueven a Old Generation.");
    }
}
```

## EXPLICACIÓN:

 * - Young Generation: Los nuevos objetos se crean en Eden Space.
 * - Minor GC: Si Eden se llena, algunos objetos se mueven a Survivor Spaces.
 * - Old Generation: Si un objeto sobrevive varias GC en Survivor, se mueve a Old Generation.
 * - Major GC: La Old Generation se limpia menos frecuentemente pero con mayor impacto.
 * - Permanent Generation (Java 7 o menos) almacenaba metadata de clases.
 * - Metaspace (Java 8+) reemplaza PermGen y se gestiona dinámicamente fuera del heap.
 
  ### Comandos útiles para monitorear la memoria:
 
 - java -XX:+PrintGCDetails -jar MiPrograma.jar  # Ver detalles de la GC
 - jstat -gc <PID> 1000  # Monitorear el uso de la memoria cada segundo
 - jvisualvm  # Interfaz gráfica para monitorear la JVM