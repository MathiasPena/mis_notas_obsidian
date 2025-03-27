```java
// Clase base o superclase
class Animal {
    // Método en la superclase
    public void hacerSonido() {
        System.out.println("El animal hace un sonido");
    }
}

// Clase derivada o subclase
class Perro extends Animal {
    // Sobrescritura del método de la superclase
    @Override
    public void hacerSonido() {
        System.out.println("El perro ladra");
    }
}

// Otra subclase derivada
class Gato extends Animal {
    // Sobrescritura del método de la superclase
    @Override
    public void hacerSonido() {
        System.out.println("El gato maúlla");
    }
}

public class OverridingDemo {
    public static void main(String[] args) {
        // Creación de objetos de las subclases
        Animal miPerro = new Perro();
        Animal miGato = new Gato();

        // Llamadas a los métodos sobrescritos
        miPerro.hacerSonido();  // Imprime: El perro ladra
        miGato.hacerSonido();    // Imprime: El gato maúlla
    }
}

```
