```java
// Clase base o superclase
class Animal {
    public void hacerSonido() {
        System.out.println("El animal hace un sonido");
    }
}

// Subclase Perro
class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("El perro ladra");
    }
}

// Subclase Gato
class Gato extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("El gato maúlla");
    }
}

// Subclase Vaca
class Vaca extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("La vaca muge");
    }
}

public class PolimorfismoDemo {
    public static void main(String[] args) {
        // Polimorfismo con referencia de tipo Animal
        Animal miAnimal = new Animal();  // Instancia de la clase base
        Animal miPerro = new Perro();    // Instancia de la subclase
        Animal miGato = new Gato();      // Instancia de la subclase
        Animal miVaca = new Vaca();     // Instancia de la subclase

        // Llamadas al mismo método, pero cada objeto tiene su propio comportamiento
        miAnimal.hacerSonido();  // Imprime: El animal hace un sonido
        miPerro.hacerSonido();   // Imprime: El perro ladra
        miGato.hacerSonido();    // Imprime: El gato maúlla
        miVaca.hacerSonido();    // Imprime: La vaca muge

        System.out.println();

        // Ejemplo de un array de Animal que almacena diferentes tipos de objetos
        Animal[] animales = { new Perro(), new Gato(), new Vaca() };

        // Llamadas polimórficas en un array
        for (Animal animal : animales) {
            animal.hacerSonido();  // El método se resuelve en tiempo de ejecución
        }
    }
}

```
