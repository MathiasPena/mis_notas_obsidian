```java
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class ManejoArchivos {
    public static void main(String[] args) {
        // Creación de un objeto File representando un archivo
        File archivo = new File("ejemplo.txt");

        // Verificar si el archivo existe
        if (archivo.exists()) {
            System.out.println("El archivo existe.");
        } else {
            System.out.println("El archivo no existe.");
        }

        // Obtener el nombre del archivo
        System.out.println("Nombre del archivo: " + archivo.getName());

        // Obtener la ruta absoluta del archivo
        System.out.println("Ruta absoluta del archivo: " + archivo.getAbsolutePath());

        // Obtener el tamaño del archivo
        System.out.println("Tamaño del archivo: " + archivo.length() + " bytes");

        // Verificar si el objeto File es un archivo o un directorio
        if (archivo.isFile()) {
            System.out.println("Es un archivo.");
        } else if (archivo.isDirectory()) {
            System.out.println("Es un directorio.");
        } else {
            System.out.println("No es un archivo ni un directorio.");
        }

        // Crear un directorio
        File directorio = new File("nuevoDirectorio");
        if (!directorio.exists()) {
            directorio.mkdir();
            System.out.println("Directorio creado: " + directorio.getAbsolutePath());
        } else {
            System.out.println("El directorio ya existe.");
        }

        // Crear un nuevo archivo
        try {
            if (archivo.createNewFile()) {
                System.out.println("Archivo creado: " + archivo.getName());
            } else {
                System.out.println("El archivo ya existe.");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Renombrar un archivo
        File archivoRenombrado = new File("nuevoNombre.txt");
        if (archivo.renameTo(archivoRenombrado)) {
            System.out.println("Archivo renombrado a: " + archivoRenombrado.getName());
        } else {
            System.out.println("No se pudo renombrar el archivo.");
        }

        // Eliminar un archivo
        if (archivoRenombrado.delete()) {
            System.out.println("Archivo eliminado.");
        } else {
            System.out.println("No se pudo eliminar el archivo.");
        }

        // Listar los archivos en un directorio
        File directorioListar = new File(".");
        String[] archivos = directorioListar.list();
        System.out.println("Archivos en el directorio actual:");
        for (String archivoDir : archivos) {
            System.out.println(archivoDir);
        }

        // Trabajar con rutas utilizando Paths (Java 7 en adelante)
        try {
            // Convertir una ruta relativa a una ruta absoluta
            java.nio.file.Path rutaRelativa = Paths.get("ejemplo.txt");
            java.nio.file.Path rutaAbsoluta = rutaRelativa.toAbsolutePath();
            System.out.println("Ruta absoluta: " + rutaAbsoluta);

            // Crear un archivo con NIO
            java.nio.file.Path rutaArchivo = Paths.get("nuevoArchivoNIO.txt");
            if (!Files.exists(rutaArchivo)) {
                Files.createFile(rutaArchivo);
                System.out.println("Archivo creado con NIO: " + rutaArchivo);
            }

            // Leer el contenido de un archivo con NIO
            java.nio.file.Path archivoALeer = Paths.get("ejemplo.txt");
            String contenido = new String(Files.readAllBytes(archivoALeer));
            System.out.println("Contenido del archivo: ");
            System.out.println(contenido);

            // Escribir en un archivo con NIO
            String nuevoContenido = "Este es un nuevo contenido para el archivo.";
            Files.write(rutaArchivo, nuevoContenido.getBytes());
            System.out.println("Nuevo contenido escrito en el archivo.");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```