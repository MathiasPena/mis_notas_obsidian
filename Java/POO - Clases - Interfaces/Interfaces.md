```java
// Definición de una interfaz
interface Vehiculo {
    // Método abstracto (por defecto todos los métodos en una interfaz son abstractos)
    void acelerar();

    // Método default (implementado en la interfaz, disponible en las clases que implementen la interfaz)
    default void frenar() {
        System.out.println("El vehículo ha frenado.");
    }

    // Método static (también implementado en la interfaz, pero se llama a través de la interfaz)
    static void encender() {
        System.out.println("El vehículo está encendido.");
    }
}

// Clase concreta que implementa la interfaz
class Coche implements Vehiculo {
    private String marca;

    // Constructor de la subclase
    public Coche(String marca) {
        this.marca = marca;
    }

    // Implementación del método abstracto
    @Override
    public void acelerar() {
        System.out.println("El coche " + marca + " está acelerando.");
    }
}

class Moto implements Vehiculo {
    private String marca;

    // Constructor de la subclase
    public Moto(String marca) {
        this.marca = marca;
    }

    // Implementación del método abstracto
    @Override
    public void acelerar() {
        System.out.println("La moto " + marca + " está acelerando.");
    }
}

public class InterfacesDemo {
    public static void main(String[] args) {
        // Crear instancias de las clases que implementan la interfaz
        Vehiculo coche = new Coche("Toyota");
        Vehiculo moto = new Moto("Yamaha");

        // Llamar al método implementado por la clase
        coche.acelerar();
        moto.acelerar();

        // Llamar al método default (compartido entre todas las clases que implementan la interfaz)
        coche.frenar();
        moto.frenar();

        // Llamar al método static de la interfaz (se llama a través de la interfaz, no de las clases)
        Vehiculo.encender();
    }
}

```
