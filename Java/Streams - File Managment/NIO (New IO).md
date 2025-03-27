```java
import java.io.IOException;
import java.nio.file.*;
import java.nio.file.attribute.BasicFileAttributes;

public class NIOEjemplo {

    public static void main(String[] args) {
        // Definir las rutas de los archivos
        Path sourcePath = Paths.get("archivo_origen.txt");
        Path destinationPath = Paths.get("archivo_destino.txt");
        Path directoryPath = Paths.get("directorio_prueba");
        
        // Copiar un archivo
        try {
            // Copiar el archivo de origen a destino
            Files.copy(sourcePath, destinationPath, StandardCopyOption.REPLACE_EXISTING);
            System.out.println("Archivo copiado exitosamente.");
        } catch (IOException e) {
            System.out.println("Error al copiar el archivo: " + e.getMessage());
        }

        // Mover un archivo
        try {
            // Mover el archivo de origen a una nueva ubicación
            Path movedPath = Paths.get("nuevo_directorio/archivo_movido.txt");
            Files.move(sourcePath, movedPath, StandardCopyOption.REPLACE_EXISTING);
            System.out.println("Archivo movido exitosamente.");
        } catch (IOException e) {
            System.out.println("Error al mover el archivo: " + e.getMessage());
        }

        // Eliminar un archivo
        try {
            Files.delete(destinationPath);  // Eliminar el archivo de destino
            System.out.println("Archivo eliminado exitosamente.");
        } catch (IOException e) {
            System.out.println("Error al eliminar el archivo: " + e.getMessage());
        }

        // Crear un directorio
        try {
            if (!Files.exists(directoryPath)) {
                Files.createDirectory(directoryPath);
                System.out.println("Directorio creado exitosamente.");
            } else {
                System.out.println("El directorio ya existe.");
            }
        } catch (IOException e) {
            System.out.println("Error al crear el directorio: " + e.getMessage());
        }

        // Recorrer un directorio y listar archivos
        try {
            Files.walkFileTree(directoryPath, new SimpleFileVisitor<Path>() {
                @Override
                public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) throws IOException {
                    System.out.println("Archivo encontrado: " + file);
                    return FileVisitResult.CONTINUE;
                }

                @Override
                public FileVisitResult visitFileFailed(Path file, IOException exc) throws IOException {
                    System.out.println("Error al acceder al archivo: " + file);
                    return FileVisitResult.CONTINUE;
                }
            });
        } catch (IOException e) {
            System.out.println("Error al recorrer el directorio: " + e.getMessage());
        }
    }
}

```