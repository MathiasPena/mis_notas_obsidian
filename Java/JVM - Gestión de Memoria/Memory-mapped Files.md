### **Memory-mapped Files (MappedByteBuffer)**

La clase `MappedByteBuffer` permite trabajar con archivos grandes sin necesidad de cargar todo el contenido en la memoria de una vez. Esto es especialmente útil cuando se manejan archivos grandes que no caben completamente en la memoria RAM, ya que permite mapear un archivo completo o parcialmente a la memoria.

#### **Conceptos Clave**

- **Memory-mapped file**: Es una técnica que permite mapear un archivo directamente en la memoria del proceso. Esto crea un "buffer" en la memoria que contiene los datos del archivo, y puede ser utilizado para leer o escribir sin tener que cargar todo el archivo en la memoria.
    
- **MappedByteBuffer**: Es un `ByteBuffer` especializado que está asociado con un archivo mapeado en memoria. Permite leer y escribir en el archivo como si fuera un arreglo de bytes en la memoria.
    

#### **Usos y Ventajas**

- **Eficiencia**: El uso de memoria mapeada permite a la JVM leer y escribir directamente en el archivo en el disco sin tener que cargar todo el archivo en memoria.
    
- **Acceso rápido**: Es muy útil cuando se necesitan leer grandes cantidades de datos de manera eficiente, como en el procesamiento de archivos grandes (por ejemplo, archivos de log, bases de datos, etc.).
    
- **Soporte para archivos grandes**: Utiliza la memoria virtual del sistema operativo, por lo que no se ve limitado por el tamaño de la RAM.
    

#### **Cómo usar Memory-mapped files**

1. **Crear un archivo mapeado en memoria**
    
    Primero, se debe abrir el archivo y mapearlo a la memoria con `MappedByteBuffer`:
    

```java
import java.nio.*;
import java.nio.channels.*;
import java.io.*;

public class MemoryMappedFileExample {
    public static void main(String[] args) throws IOException {
        // Abrir el archivo
        RandomAccessFile file = new RandomAccessFile("archivo_grande.txt", "rw");

        // Obtener el canal del archivo
        FileChannel channel = file.getChannel();

        // Mapeo del archivo a memoria (tamaño del archivo en bytes)
        MappedByteBuffer buffer = channel.map(FileChannel.MapMode.READ_WRITE, 0, file.length());

        // Leer datos desde el archivo mapeado
        while (buffer.hasRemaining()) {
            System.out.print((char) buffer.get());
        }

        // Escribir datos en el archivo mapeado
        String dataToWrite = "Añadiendo datos al archivo!";
        buffer.position(buffer.limit()); // Mover el cursor al final
        buffer.put(dataToWrite.getBytes());

        // Cerrar el archivo
        file.close();
    }
}
```

- **`channel.map()`**: Este método mapea el archivo al espacio de direcciones de la memoria. El primer parámetro es el tipo de acceso (`READ_WRITE`), el segundo es la posición inicial en el archivo, y el tercero es el tamaño del archivo o el número de bytes a mapear.
    
- **`MappedByteBuffer`**: Este objeto se utiliza para leer y escribir en el archivo mapeado.
    

2. **Acceso a los datos**
    
    Se pueden leer y escribir datos de la misma forma que con un `ByteBuffer` tradicional. Ejemplo:
    
    - **Leer**: `buffer.get()` lee un byte del archivo mapeado.
        
    - **Escribir**: `buffer.put(byte)` escribe un byte al archivo mapeado.
        

#### **Consideraciones**

- **Consistencia de los datos**: Los datos escritos en el `MappedByteBuffer` se sincronizan automáticamente con el archivo cuando el buffer se actualiza, pero también puedes forzar la sincronización manualmente usando el método `force()`:
    
    ```java
    buffer.force();  // Asegura que los cambios se escriban en el archivo
    ```
    
- **Escalabilidad**: Puedes mapear grandes archivos en varias partes. Si el archivo es más grande que la memoria disponible, puedes mapear solo una parte del archivo a la vez.
    
- **Limitaciones**: Aunque el acceso a los archivos mediante memoria mapeada es eficiente, no es adecuado para todos los casos, como cuando se necesitan operaciones de lectura/escritura pequeñas y frecuentes.
    

#### **Ejemplo de mapeo parcial de un archivo**

Si el archivo es muy grande y solo necesitas leer una porción de él, puedes mapear una parte del archivo en lugar de todo el archivo:

```java
import java.nio.*;
import java.nio.channels.*;
import java.io.*;

public class MemoryMappedFilePartialExample {
    public static void main(String[] args) throws IOException {
        RandomAccessFile file = new RandomAccessFile("archivo_grande.txt", "rw");
        FileChannel channel = file.getChannel();

        // Mapeo solo una parte del archivo (por ejemplo, los primeros 1000 bytes)
        MappedByteBuffer buffer = channel.map(FileChannel.MapMode.READ_ONLY, 0, 1000);

        // Leer los datos mapeados
        while (buffer.hasRemaining()) {
            System.out.print((char) buffer.get());
        }

        file.close();
    }
}
```

#### **Cierre del MappedByteBuffer**

Es importante cerrar correctamente el canal de archivos y liberar el buffer mapeado cuando ya no se necesite. Sin embargo, el buffer mapeado generalmente es liberado automáticamente por la JVM cuando ya no es accesible, pero se recomienda realizar el cierre adecuado.

#### **Conclusión**

La clase `MappedByteBuffer` de Java proporciona una forma eficiente de trabajar con archivos grandes sin tener que cargar todo el archivo en la memoria. Esto es útil para aplicaciones que necesitan manipular grandes cantidades de datos de forma eficiente, como bases de datos o procesamiento de grandes archivos de texto. El acceso a los archivos mapeados en memoria puede ser más rápido que leerlos o escribirlos en el disco utilizando técnicas tradicionales.