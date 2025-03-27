```java
import java.io.*;

public class BinaryDataStreamExample {

    public static void main(String[] args) {
        // Ruta del archivo binario
        String filePath = "archivo_binario.dat";
        
        // Escribir datos binarios usando FileOutputStream
        try (FileOutputStream fos = new FileOutputStream(filePath)) {
            // Escribir un byte
            fos.write(65); // El valor 65 representa la letra 'A' en ASCII
            
            // Escribir un arreglo de bytes
            byte[] byteArray = { 66, 67, 68 }; // Representa 'B', 'C', 'D'
            fos.write(byteArray);
            
            // Escribir más de un byte en un solo bloque
            fos.write(byteArray, 0, 2); // Escribe solo los primeros dos bytes (B y C)
            
            System.out.println("Datos binarios escritos en el archivo.");
        } catch (IOException e) {
            System.out.println("Error al escribir el archivo: " + e.getMessage());
        }
        
        // Leer datos binarios usando FileInputStream
        try (FileInputStream fis = new FileInputStream(filePath)) {
            // Leer el primer byte
            int byteData = fis.read();
            System.out.println("Primer byte leído: " + byteData); // Imprime el valor numérico (65)
            
            // Leer todo el contenido del archivo
            int byteContent;
            while ((byteContent = fis.read()) != -1) {
                System.out.print((char) byteContent + " "); // Imprime los caracteres correspondientes
            }
            System.out.println("\nDatos binarios leídos del archivo.");
        } catch (IOException e) {
            System.out.println("Error al leer el archivo: " + e.getMessage());
        }
    }
}

```
