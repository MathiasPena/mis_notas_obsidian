```java
import java.io.*;
import java.util.zip.*;

public class GzipCompressionExample {

    public static void main(String[] args) {
        // Rutas de archivo de entrada y archivo comprimido
        String inputFile = "archivo_original.txt";
        String compressedFile = "archivo_comprimido.gz";
        String decompressedFile = "archivo_descomprimido.txt";
        
        // Escribir datos a un archivo comprimido usando GZIPOutputStream
        try (FileOutputStream fos = new FileOutputStream(compressedFile);
             GZIPOutputStream gzipOS = new GZIPOutputStream(fos);
             BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(gzipOS))) {

            // Escribir datos en el archivo comprimido
            writer.write("Este es un archivo comprimido con GZIP.");
            writer.newLine();
            writer.write("Esto es un segundo párrafo.");
            
            System.out.println("Archivo comprimido creado: " + compressedFile);
        } catch (IOException e) {
            System.out.println("Error al comprimir el archivo: " + e.getMessage());
        }

        // Leer datos de un archivo comprimido usando GZIPInputStream
        try (FileInputStream fis = new FileInputStream(compressedFile);
             GZIPInputStream gzipIS = new GZIPInputStream(fis);
             BufferedReader reader = new BufferedReader(new InputStreamReader(gzipIS))) {

            // Leer el contenido descomprimido
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
            
            System.out.println("Archivo descomprimido leído.");
        } catch (IOException e) {
            System.out.println("Error al descomprimir el archivo: " + e.getMessage());
        }
        
        // Descomprimir archivo y guardar en otro archivo (ejemplo de descompresión completa)
        try (FileInputStream fis = new FileInputStream(compressedFile);
             GZIPInputStream gzipIS = new GZIPInputStream(fis);
             FileOutputStream fos = new FileOutputStream(decompressedFile)) {

            byte[] buffer = new byte[1024];
            int length;
            while ((length = gzipIS.read(buffer)) != -1) {
                fos.write(buffer, 0, length);
            }
            
            System.out.println("Archivo descomprimido a: " + decompressedFile);
        } catch (IOException e) {
            System.out.println("Error al descomprimir el archivo: " + e.getMessage());
        }
    }
}

```
