```java
import java.io.*;
import java.nio.file.*;
import java.nio.file.attribute.*;

public class DirectoryManagementExample {

    public static void main(String[] args) {
        // Directorio a crear, renombrar o eliminar
        String dirPath = "nuevo_directorio";
        String renamedDirPath = "directorio_renombrado";
        
        // Crear un directorio usando File
        File dir = new File(dirPath);
        if (!dir.exists()) {
            boolean created = dir.mkdir();  // Crear un directorio
            if (created) {
                System.out.println("Directorio creado: " + dirPath);
            } else {
                System.out.println("No se pudo crear el directorio.");
            }
        } else {
            System.out.println("El directorio ya existe.");
        }
        
        // Renombrar el directorio usando File
        File renamedDir = new File(renamedDirPath);
        if (dir.renameTo(renamedDir)) {
            System.out.println("Directorio renombrado a: " + renamedDirPath);
        } else {
            System.out.println("No se pudo renombrar el directorio.");
        }

        // Eliminar un directorio vacío usando File
        if (renamedDir.exists() && renamedDir.isDirectory()) {
            boolean deleted = renamedDir.delete();
            if (deleted) {
                System.out.println("Directorio eliminado: " + renamedDirPath);
            } else {
                System.out.println("No se pudo eliminar el directorio.");
            }
        }

        // Usar Files para crear un directorio
        Path path = Paths.get("directorio_files");
        try {
            Files.createDirectory(path);
            System.out.println("Directorio creado usando Files: " + path.toString());
        } catch (IOException e) {
            System.out.println("Error al crear directorio con Files: " + e.getMessage());
        }

        // Usar Files para renombrar un directorio
        Path newPath = Paths.get("nuevo_directorio_renombrado");
        try {
            Files.move(path, newPath);  // Renombrar el directorio
            System.out.println("Directorio renombrado con Files: " + newPath.toString());
        } catch (IOException e) {
            System.out.println("Error al renombrar el directorio con Files: " + e.getMessage());
        }

        // Usar Files para eliminar un directorio vacío
        try {
            Files.delete(newPath);  // Eliminar el directorio
            System.out.println("Directorio eliminado con Files: " + newPath.toString());
        } catch (IOException e) {
            System.out.println("Error al eliminar el directorio con Files: " + e.getMessage());
        }

        // Listar archivos dentro de un directorio usando DirectoryStream
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(Paths.get("."))) {
            System.out.println("Archivos en el directorio actual:");
            for (Path entry : stream) {
                System.out.println(entry.getFileName());
            }
        } catch (IOException e) {
            System.out.println("Error al listar los archivos: " + e.getMessage());
        }
    }
}

```