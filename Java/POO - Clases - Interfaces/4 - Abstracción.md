```java
// Clase abstracta
abstract class Vehiculo {
    // Atributos comunes para todas las clases
    protected String marca;
    protected int velocidad;

    // Constructor para inicializar los atributos
    public Vehiculo(String marca, int velocidad) {
        this.marca = marca;
        this.velocidad = velocidad;
    }

    // Método abstracto (sin implementación), las subclases deben implementarlo
    public abstract void acelerar();

    // Método común, con implementación
    public void frenar() {
        System.out.println("El vehículo ha frenado.");
    }

    // Método para mostrar información del vehículo
    public void mostrarInfo() {
        System.out.println("Marca: " + marca);
        System.out.println("Velocidad: " + velocidad);
    }
}

// Clase concreta que hereda de Vehiculo
class Coche extends Vehiculo {
    // Constructor de la subclase
    public Coche(String marca, int velocidad) {
        super(marca, velocidad);
    }

    // Implementación del método abstracto
    @Override
    public void acelerar() {
        System.out.println("El coche está acelerando a " + velocidad + " km/h.");
    }
}

// Otra clase concreta que hereda de Vehiculo
class Moto extends Vehiculo {
    // Constructor de la subclase
    public Moto(String marca, int velocidad) {
        super(marca, velocidad);
    }

    // Implementación del método abstracto
    @Override
    public void acelerar() {
        System.out.println("La moto está acelerando a " + velocidad + " km/h.");
    }
}

public class AbstraccionDemo {
    public static void main(String[] args) {
        // Crear instancias de las subclases
        Vehiculo miCoche = new Coche("Toyota", 180);
        Vehiculo miMoto = new Moto("Yamaha", 150);

        // Llamadas a los métodos de la clase base
        miCoche.mostrarInfo();
        miCoche.acelerar();
        miCoche.frenar();

        System.out.println();

        miMoto.mostrarInfo();
        miMoto.acelerar();
        miMoto.frenar();
    }
}

```
