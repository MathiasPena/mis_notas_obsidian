```java
import java.io.*;

class Persona implements Serializable {
    private String nombre;
    private int edad;

    // Constructor
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    // Getter y Setter
    public String getNombre() {
        return nombre;
    }

    public int getEdad() {
        return edad;
    }

    // Método para mostrar información de la persona
    public void mostrarInfo() {
        System.out.println("Nombre: " + nombre + ", Edad: " + edad);
    }
}

public class SerializacionObjeto {
    public static void main(String[] args) {
        // Crear un objeto de la clase Persona
        Persona persona = new Persona("Juan", 30);

        // Ruta del archivo donde se serializará el objeto
        File archivo = new File("persona.ser");

        // Serialización: Guardar el objeto en un archivo
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(archivo))) {
            oos.writeObject(persona);
            System.out.println("Objeto serializado correctamente.");
        } catch (IOException e) {
            System.err.println("Error al serializar el objeto: " + e.getMessage());
        }

        // Deserialización: Leer el objeto del archivo
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream(archivo))) {
            Persona personaDeserializada = (Persona) ois.readObject();
            System.out.println("Objeto deserializado correctamente.");
            personaDeserializada.mostrarInfo(); // Mostrar información del objeto deserializado
        } catch (IOException | ClassNotFoundException e) {
            System.err.println("Error al deserializar el objeto: " + e.getMessage());
        }
    }
}

```
