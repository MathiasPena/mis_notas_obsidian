```java
import java.io.*;

public class LecturaConFileReaderBufferedReader {
    public static void main(String[] args) {
        // Ruta del archivo a leer
        File archivo = new File("ejemplo.txt");

        // Verificación de si el archivo existe
        if (!archivo.exists()) {
            System.out.println("El archivo no existe.");
            return;
        }

        // Lectura con FileReader y BufferedReader
        try {
            // 1. Crear un FileReader que lee el archivo de texto
            FileReader fileReader = new FileReader(archivo);

            // 2. Envolver el FileReader en un BufferedReader para optimizar la lectura
            BufferedReader bufferedReader = new BufferedReader(fileReader);
            
            // 3. Leer línea por línea usando readLine()
            String linea;
            System.out.println("Leyendo archivo con FileReader y BufferedReader:");
            while ((linea = bufferedReader.readLine()) != null) {
                System.out.println(linea); // Imprimir cada línea leída
            }

            // 4. Cerrar los flujos de lectura para liberar los recursos
            bufferedReader.close();
            fileReader.close();

        } catch (FileNotFoundException e) {
            // Este error ocurre si el archivo no se encuentra en la ubicación especificada
            System.err.println("Archivo no encontrado: " + e.getMessage());
        } catch (IOException e) {
            // Este error ocurre si hay problemas al leer el archivo
            System.err.println("Error de lectura: " + e.getMessage());
        }
    }
}

```