```java
import java.io.*;

public class EscrituraArchivoFileWriter {
    public static void main(String[] args) {
        // Ruta del archivo donde se escribirá el contenido
        File archivo = new File("escritura_filewriter.txt");

        // Uso de FileWriter para escribir en el archivo
        try (FileWriter writer = new FileWriter(archivo)) {
            // Escribir una línea en el archivo
            writer.write("Este es un ejemplo de escritura con FileWriter.\n");
            writer.write("Otro texto en una nueva línea.\n");

            System.out.println("Contenido escrito con FileWriter.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }
}

import java.io.*;

public class EscrituraConFileWriterConSaltos {
    public static void main(String[] args) {
        // Ruta del archivo donde se escribirá el contenido
        File archivo = new File("escritura_filewriter_saltos.txt");

        // Uso de FileWriter para escribir con saltos de línea
        try (FileWriter writer = new FileWriter(archivo)) {
            // Escribir con saltos de línea
            writer.write("Este es un texto con saltos de línea.\n");
            writer.write("\n"); // Salto de línea explícito
            writer.write("Otro bloque de texto después de un salto de línea.\n");

            System.out.println("Contenido escrito con saltos de línea usando FileWriter.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }
}

```

```java
import java.io.*;

public class EscrituraArchivoBufferedWriter {
    public static void main(String[] args) {
        // Ruta del archivo donde se escribirá el contenido
        File archivo = new File("escritura_bufferedwriter.txt");

        // Uso de BufferedWriter para escribir en el archivo
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(archivo))) {
            // Escribir líneas de texto en el archivo con BufferedWriter
            writer.write("Este es un ejemplo de escritura con BufferedWriter.\n");
            writer.write("BufferedWriter es más eficiente para escribir grandes cantidades de datos.\n");

            // Asegurarse de que los datos se escriban en el archivo
            writer.flush();

            System.out.println("Contenido escrito con BufferedWriter.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }
}

import java.io.*;

public class EscrituraConBufferedWriterConFormato {
    public static void main(String[] args) {
        // Ruta del archivo donde se escribirá el contenido
        File archivo = new File("escritura_bufferedwriter_formato.txt");

        // Uso de BufferedWriter para escribir con formato
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(archivo))) {
            // Escribir con formato usando el método write
            writer.write(String.format("Nombre: %s, Edad: %d, Altura: %.2f\n", "Carlos", 28, 1.85));
            writer.write(String.format("Nombre: %s, Edad: %d, Altura: %.2f\n", "Ana", 22, 1.70));

            // Asegurarse de que los datos se escriban en el archivo
            writer.flush();

            System.out.println("Contenido escrito con formato con BufferedWriter.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }
}

```

```java
import java.io.*;

public class EscrituraArchivoPrintWriter {
    public static void main(String[] args) {
        // Ruta del archivo donde se escribirá el contenido
        File archivo = new File("escritura_printwriter.txt");

        // Uso de PrintWriter para escribir en el archivo
        try (PrintWriter writer = new PrintWriter(new FileWriter(archivo))) {
            // Escribir en el archivo utilizando PrintWriter
            writer.println("Este es un ejemplo de escritura con PrintWriter.");
            writer.println("PrintWriter proporciona métodos adicionales como print y println.");

            System.out.println("Contenido escrito con PrintWriter.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }
}


import java.io.*;

public class EscrituraConPrintWriterConFormato {
    public static void main(String[] args) {
        // Ruta del archivo donde se escribirá el contenido
        File archivo = new File("escritura_printwriter_formato.txt");

        // Uso de PrintWriter para escribir con formato
        try (PrintWriter writer = new PrintWriter(new FileWriter(archivo))) {
            // Escribir con formato usando printf
            writer.printf("Nombre: %s, Edad: %d, Altura: %.2f\n", "Juan", 30, 1.75);
            writer.printf("Nombre: %s, Edad: %d, Altura: %.2f\n", "María", 25, 1.60);

            System.out.println("Contenido escrito con formato con PrintWriter.");
        } catch (IOException e) {
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }
}

```