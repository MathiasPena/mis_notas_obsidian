```java
// Clase base o superclase
class Animal {
    public void hacerSonido() {
        System.out.println("El animal hace un sonido");
    }
}

// Subclase Perro
class Perro extends Animal {
    public void hacerSonido() {
        System.out.println("El perro ladra");
    }
}

// Subclase Gato
class Gato extends Animal {
    public void hacerSonido() {
        System.out.println("El gato maúlla");
    }
}

public class CastingDemo {
    public static void main(String[] args) {
        // Upcasting: convertir un objeto de una subclase a su clase base
        Animal miPerro = new Perro();  // Upcasting automático
        Animal miGato = new Gato();     // Upcasting automático

        // Llamada al método hacerSonido() usando referencias de tipo Animal
        miPerro.hacerSonido();  // Imprime: El perro ladra
        miGato.hacerSonido();   // Imprime: El gato maúlla

        // Downcasting: convertir una referencia de tipo Animal a una referencia de subclase
        Perro perro = (Perro) miPerro;  // Downcasting explícito
        Gato gato = (Gato) miGato;      // Downcasting explícito

        // Llamada al método hacerSonido() con las referencias convertidas
        perro.hacerSonido();  // Imprime: El perro ladra
        gato.hacerSonido();   // Imprime: El gato maúlla

        // Ejemplo de un cast incorrecto (provocará ClassCastException en tiempo de ejecución)
        try {
            Gato perroComoGato = (Gato) miPerro;  // Esto lanzará una excepción
            perroComoGato.hacerSonido();
        } catch (ClassCastException e) {
            System.out.println("Error de conversión: " + e.getMessage());
        }
    }
}

```
