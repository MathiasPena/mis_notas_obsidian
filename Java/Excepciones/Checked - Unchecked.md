```java
// Ejemplo de excepción checked (compilación obliga a manejarla)
class ExcepcionChecked extends Exception {
    public ExcepcionChecked(String mensaje) {
        super(mensaje);
    }
}

// Ejemplo de excepción unchecked (no es obligatorio manejarla)
class ExcepcionUnchecked extends RuntimeException {
    public ExcepcionUnchecked(String mensaje) {
        super(mensaje);
    }
}

public class CheckedUncheckedDemo {
    public static void main(String[] args) {
        // Manejo de una excepción checked
        try {
            metodoConChecked();
        } catch (ExcepcionChecked e) {
            System.out.println("Checked Exception capturada: " + e.getMessage());
        }

        // Ejemplo de excepción unchecked (no requiere try-catch obligatorio)
        metodoConUnchecked(); // Si no la manejamos, el programa se detiene en tiempo de ejecución
    }

    // Método que lanza una excepción checked
    public static void metodoConChecked() throws ExcepcionChecked {
        throw new ExcepcionChecked("Esto es una excepción checked.");
    }

    // Método que lanza una excepción unchecked
    public static void metodoConUnchecked() {
        throw new ExcepcionUnchecked("Esto es una excepción unchecked.");
    }
}

```
