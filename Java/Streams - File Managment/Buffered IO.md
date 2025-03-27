```java
import java.io.*;

public class BufferedIOExample {

    public static void main(String[] args) {
        // Ruta del archivo de origen (para leer)
        String sourceFile = "archivo_grande_lectura.txt";
        // Ruta del archivo de destino (para escribir)
        String destinationFile = "archivo_grande_escritura.txt";

        // Leer archivo usando BufferedReader
        try (BufferedReader reader = new BufferedReader(new FileReader(sourceFile))) {
            String line;
            long startTime = System.currentTimeMillis();
            
            while ((line = reader.readLine()) != null) {
                // Procesar cada línea del archivo
                // Aquí solo estamos mostrando la línea en consola para el ejemplo
                System.out.println(line);
            }
            
            long endTime = System.currentTimeMillis();
            System.out.println("Tiempo de lectura con BufferedReader: " + (endTime - startTime) + " ms");
        } catch (IOException e) {
            System.out.println("Error al leer el archivo: " + e.getMessage());
        }

        // Escribir archivo usando BufferedWriter
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(destinationFile))) {
            String content = "Este es un contenido de ejemplo para escribir en un archivo grande.\n";
            long startTime = System.currentTimeMillis();
            
            // Escribir múltiples líneas al archivo
            for (int i = 0; i < 100000; i++) {
                writer.write(content + i);
                writer.newLine();  // Para separar las líneas
            }
            
            long endTime = System.currentTimeMillis();
            System.out.println("Tiempo de escritura con BufferedWriter: " + (endTime - startTime) + " ms");
        } catch (IOException e) {
            System.out.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }
}

```