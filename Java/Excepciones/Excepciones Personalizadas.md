```java
// Definición de una excepción personalizada que extiende Exception
class MiExcepcion extends Exception {
    public MiExcepcion(String mensaje) {
        super(mensaje);
    }
}

// Otra excepción personalizada que extiende RuntimeException (unchecked)
class MiExcepcionRuntime extends RuntimeException {
    public MiExcepcionRuntime(String mensaje) {
        super(mensaje);
    }
}

public class ExcepcionesPersonalizadasDemo {
    public static void main(String[] args) {
        try {
            lanzarMiExcepcion();
        } catch (MiExcepcion e) {
            System.out.println("Excepción capturada: " + e.getMessage());
        }

        try {
            lanzarMiExcepcionRuntime(); // No requiere catch obligatorio, es unchecked
        } catch (MiExcepcionRuntime e) {
            System.out.println("Excepción Runtime capturada: " + e.getMessage());
        }
    }

    // Método que lanza una excepción personalizada checked
    public static void lanzarMiExcepcion() throws MiExcepcion {
        throw new MiExcepcion("Esto es una excepción personalizada checked.");
    }

    // Método que lanza una excepción personalizada unchecked
    public static void lanzarMiExcepcionRuntime() {
        throw new MiExcepcionRuntime("Esto es una excepción personalizada unchecked.");
    }
}

```
