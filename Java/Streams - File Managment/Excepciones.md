```java
import java.io.*;

public class ManejoExcepcionesArchivos {
    public static void main(String[] args) {
        // Ejemplo de manejo de excepciones al leer un archivo con FileReader y BufferedReader
        try {
            // Intentando abrir el archivo
            FileReader fileReader = new FileReader("archivo.txt");
            BufferedReader bufferedReader = new BufferedReader(fileReader);
            
            String linea;
            while ((linea = bufferedReader.readLine()) != null) {
                System.out.println(linea);
            }
            
            // Cerramos el BufferedReader
            bufferedReader.close();
        } catch (FileNotFoundException e) {
            System.out.println("El archivo no se encontró: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("Error de entrada/salida: " + e.getMessage());
        } finally {
            System.out.println("Operación de lectura terminada.");
        }

        // Ejemplo de manejo de excepciones al escribir en un archivo con FileWriter y BufferedWriter
        try {
            // Intentamos abrir el archivo para escritura
            FileWriter fileWriter = new FileWriter("archivo_salida.txt");
            BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);
            
            bufferedWriter.write("Este es un ejemplo de escritura en archivo.");
            bufferedWriter.newLine();
            bufferedWriter.write("Otra línea de texto.");
            
            // Cerramos el BufferedWriter
            bufferedWriter.close();
        } catch (IOException e) {
            System.out.println("Error al escribir el archivo: " + e.getMessage());
        } finally {
            System.out.println("Operación de escritura terminada.");
        }
        
        // Ejemplo de manejo de excepciones con Scanner al leer de un archivo
        try {
            Scanner scanner = new Scanner(new File("archivo_entrada.txt"));
            while (scanner.hasNextLine()) {
                System.out.println(scanner.nextLine());
            }
            scanner.close();
        } catch (FileNotFoundException e) {
            System.out.println("Archivo no encontrado: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("Error de entrada/salida con Scanner: " + e.getMessage());
        } finally {
            System.out.println("Operación con Scanner terminada.");
        }
    }
}

```