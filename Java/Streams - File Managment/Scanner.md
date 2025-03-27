```java
import java.io.*;
import java.util.*;

public class LecturaConScanner {
    public static void main(String[] args) {
        // Ruta del archivo a leer
        File archivo = new File("ejemplo.txt");

        // Verificación de si el archivo existe
        if (!archivo.exists()) {
            System.out.println("El archivo no existe.");
            return;
        }

        // Uso de Scanner para leer el archivo
        try {
            // Crear un Scanner que lee el archivo
            Scanner scanner = new Scanner(archivo);

            // Leer línea por línea
            System.out.println("Leyendo archivo con Scanner:");
            while (scanner.hasNextLine()) {
                String linea = scanner.nextLine();  // Lee una línea completa
                System.out.println(linea);
            }

            // Cerrar el scanner para liberar recursos
            scanner.close();

        } catch (FileNotFoundException e) {
            // Este error ocurre si el archivo no se encuentra en la ubicación especificada
            System.err.println("Archivo no encontrado: " + e.getMessage());
        }
    }
}

```

```java
import java.io.*;
import java.util.*;

public class LecturaScannerTipos {
    public static void main(String[] args) {
        // Ruta del archivo a leer
        File archivo = new File("numeros.txt");

        // Verificación de si el archivo existe
        if (!archivo.exists()) {
            System.out.println("El archivo no existe.");
            return;
        }

        // Uso de Scanner para leer datos de diferentes tipos
        try {
            // Crear un Scanner para leer desde el archivo
            Scanner scanner = new Scanner(archivo);

            // Leer y procesar datos del archivo
            while (scanner.hasNext()) {
                if (scanner.hasNextInt()) {
                    int numero = scanner.nextInt();  // Lee un entero
                    System.out.println("Número entero: " + numero);
                } else if (scanner.hasNextDouble()) {
                    double decimal = scanner.nextDouble();  // Lee un número decimal
                    System.out.println("Número decimal: " + decimal);
                } else {
                    String texto = scanner.next();  // Lee un String
                    System.out.println("Texto: " + texto);
                }
            }

            // Cerrar el scanner para liberar recursos
            scanner.close();

        } catch (FileNotFoundException e) {
            System.err.println("Archivo no encontrado: " + e.getMessage());
        }
    }
}

```

```java
import java.io.*;
import java.util.*;

public class LecturaScannerCompleta {
    public static void main(String[] args) {
        // Ruta del archivo a leer
        File archivo = new File("archivo_completo.txt");

        // Verificación de si el archivo existe
        if (!archivo.exists()) {
            System.out.println("El archivo no existe.");
            return;
        }

        // Uso de Scanner para leer todo el archivo como una sola cadena
        try {
            // Crear un Scanner para leer el archivo
            Scanner scanner = new Scanner(archivo);

            // Leer todo el contenido del archivo y almacenarlo en una sola cadena
            String contenido = scanner.useDelimiter("\\A").next(); // Usa el delimitador de "fin de archivo" (\\A)

            // Imprimir todo el contenido
            System.out.println("Contenido del archivo completo:");
            System.out.println(contenido);

            // Cerrar el scanner para liberar recursos
            scanner.close();

        } catch (FileNotFoundException e) {
            System.err.println("Archivo no encontrado: " + e.getMessage());
        }
    }
}

```

```java
import java.util.*;

public class LecturaScannerConsola {
    public static void main(String[] args) {
        // Crear un objeto Scanner para leer desde la consola
        Scanner scanner = new Scanner(System.in);

        // Leer una cadena
        System.out.print("Introduce tu nombre: ");
        String nombre = scanner.nextLine();
        System.out.println("Hola, " + nombre);

        // Leer un número entero
        System.out.print("Introduce tu edad: ");
        int edad = scanner.nextInt();
        System.out.println("Tienes " + edad + " años.");

        // Leer un número decimal
        System.out.print("Introduce tu altura: ");
        double altura = scanner.nextDouble();
        System.out.println("Tu altura es " + altura + " metros.");

        // Cerrar el scanner para liberar recursos
        scanner.close();
    }
}

```

```java
import java.io.*;
import java.util.*;

public class LecturaConScannerConExcepciones {
    public static void main(String[] args) {
        File archivo = new File("datos.txt");

        try {
            Scanner scanner = new Scanner(archivo);

            while (scanner.hasNext()) {
                if (scanner.hasNextInt()) {
                    int numero = scanner.nextInt();
                    System.out.println("Número leído: " + numero);
                } else {
                    String palabra = scanner.next();
                    System.out.println("Palabra leída: " + palabra);
                }
            }

            scanner.close();

        } catch (FileNotFoundException e) {
            System.err.println("Archivo no encontrado: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Error al leer el archivo: " + e.getMessage());
        }
    }
}

```
