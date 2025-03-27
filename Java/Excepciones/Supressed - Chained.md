```java
import java.io.*; // Importamos para manejar excepciones de IO

public class ExcepcionesAvanzadasDemo {
    public static void main(String[] args) {
        // Ejemplo de Suppressed Exceptions con try-with-resources
        try (Recurso recurso = new Recurso()) {
            recurso.accion();
        } catch (Exception e) {
            System.out.println("Excepción principal: " + e.getMessage());
            for (Throwable suprimida : e.getSuppressed()) {
                System.out.println("Excepción suprimida: " + suprimida.getMessage());
            }
        }

        // Ejemplo de Chained Exceptions con initCause
        try {
            metodoQueEncadena();
        } catch (Exception e) {
            System.out.println("Excepción capturada: " + e.getMessage());
            System.out.println("Causa: " + e.getCause().getMessage());
        }
    }

    // Clase para try-with-resources (simula un recurso que lanza excepciones)
    static class Recurso implements AutoCloseable {
        public void accion() throws Exception {
            throw new Exception("Error en la acción principal");
        }

        @Override
        public void close() throws Exception {
            throw new Exception("Error al cerrar el recurso");
        }
    }

    // Método que encadena excepciones
    public static void metodoQueEncadena() throws Exception {
        try {
            throw new IOException("Error de IO inicial");
        } catch (IOException e) {
            Exception nuevaExcepcion = new Exception("Nueva excepción con causa");
            nuevaExcepcion.initCause(e); // Encadena la causa original
            throw nuevaExcepcion;
        }
    }
}

```
