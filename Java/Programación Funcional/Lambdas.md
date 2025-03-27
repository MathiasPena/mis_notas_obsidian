
```java
import java.util.*;
import java.util.function.*;

// Funciones de ejemplo para cubrir diferentes usos de Lambdas en Java

public class LambdasExample {

    public static void main(String[] args) {

        // 1. Uso básico de lambda con una interfaz funcional
        // Interfaz funcional con un solo método que recibe un parámetro y no retorna nada
        @FunctionalInterface
        interface Imprimir {
            void imprimirMensaje(String mensaje);
        }

        Imprimir imprimirMensaje = (mensaje) -> System.out.println(mensaje);
        imprimirMensaje.imprimirMensaje("¡Hola desde la lambda!"); // Imprime mensaje

        // 2. Uso de BiFunction: toma dos parámetros y devuelve un resultado
        BiFunction<Integer, Integer, Integer> sumar = (a, b) -> a + b;
        System.out.println("Resultado de la suma: " + sumar.apply(5, 3)); // Imprime "8"

        // 3. Uso de Predicate: para probar si un valor cumple con una condición
        Predicate<Integer> esMayorQue10 = (n) -> n > 10;
        System.out.println("¿Es mayor que 10?: " + esMayorQue10.test(15)); // true

        // 4. Uso de Function: convierte un valor a otro tipo (como String a Integer)
        Function<String, Integer> longitud = (s) -> s.length();
        System.out.println("Longitud del string 'Java': " + longitud.apply("Java")); // 4

        // 5. Uso de Consumer: acepta un parámetro y realiza una operación, sin devolver nada
        List<String> lista = Arrays.asList("Java", "Python", "C++");
        Consumer<String> mostrarLista = (elemento) -> System.out.println(elemento);
        lista.forEach(mostrarLista); // Imprime cada elemento de la lista

        // 6. Uso de Supplier: genera un valor sin necesidad de parámetros
        Supplier<Integer> obtenerNumeroAleatorio = () -> (int) (Math.random() * 100);
        System.out.println("Número aleatorio: " + obtenerNumeroAleatorio.get()); // Imprime un número aleatorio

        // 7. Uso de UnaryOperator: toma un solo parámetro y lo devuelve transformado
        UnaryOperator<Integer> cuadrado = (n) -> n * n;
        System.out.println("El cuadrado de 5 es: " + cuadrado.apply(5)); // 25

        // 8. Uso de BinaryOperator: toma dos parámetros del mismo tipo y devuelve un valor del mismo tipo
        BinaryOperator<Integer> multiplicar = (a, b) -> a * b;
        System.out.println("El resultado de multiplicar 4 y 5 es: " + multiplicar.apply(4, 5)); // 20

        // 9. Uso de referencias a métodos (method reference)
        lista.forEach(System.out::println); // Referencia al método println de System.out

        // 10. Uso de operaciones con Streams y Lambdas (filtrar, mapear, ordenar)
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Filtrar números mayores que 5 y multiplicar cada uno por 2
        List<Integer> resultado = numeros.stream()
                .filter(n -> n > 5) // Filtrar
                .map(n -> n * 2)    // Mapear (multiplicar por 2)
                .collect(Collectors.toList()); // Colectar en lista

        System.out.println("Resultado del procesamiento con Streams: " + resultado); // [12, 14, 16, 18, 20]

        // 11. Uso de Lambdas en la interfaz Comparable para ordenar objetos personalizados
        List<Persona> personas = Arrays.asList(new Persona("Juan", 30), new Persona("Ana", 25), new Persona("Pedro", 35));
        
        // Ordenar por edad usando una lambda
        Collections.sort(personas, (p1, p2) -> Integer.compare(p1.getEdad(), p2.getEdad()));
        
        System.out.println("Lista ordenada por edad:");
        personas.forEach(p -> System.out.println(p.getNombre() + " - " + p.getEdad()));

        // 12. Uso de Lambdas en la interfaz Comparator para ordenar objetos personalizados en orden inverso
        Collections.sort(personas, (p1, p2) -> Integer.compare(p2.getEdad(), p1.getEdad())); // Orden inverso

        System.out.println("Lista ordenada por edad (inverso):");
        personas.forEach(p -> System.out.println(p.getNombre() + " - " + p.getEdad()));
    }
    
    // Clase ejemplo de Persona para los ejemplos de ordenación
    static class Persona {
        private String nombre;
        private int edad;

        public Persona(String nombre, int edad) {
            this.nombre = nombre;
            this.edad = edad;
        }

        public String getNombre() {
            return nombre;
        }

        public int getEdad() {
            return edad;
        }
    }
}

```

- **`Imprimir`**: Ejemplo básico de lambda que toma un parámetro y realiza una acción (en este caso, imprimir).
    
- **`BiFunction`**: Función que recibe dos parámetros y devuelve un resultado (como una suma).
    
- **`Predicate`**: Verifica una condición booleana sobre un valor (como si un número es mayor que 10).
    
- **`Function`**: Transforma un valor a otro tipo (en este caso, la longitud de un string).
    
- **`Consumer`**: Procesa cada elemento de una lista sin devolver un resultado (como imprimir elementos).
    
- **`Supplier`**: Genera un valor sin necesidad de parámetros (como generar un número aleatorio).
    
- **`UnaryOperator`**: Función que toma un solo parámetro y lo transforma (como elevar al cuadrado un número).
    
- **`BinaryOperator`**: Función que toma dos parámetros del mismo tipo y devuelve un resultado (como multiplicar dos números).
    
- **`Method References`**: Refleja una forma más compacta de utilizar lambdas, llamando a un método ya existente en vez de escribir el cuerpo completo de la lambda.
    
- **Streams con Lambdas**: Permite manipular colecciones con operaciones como `filter`, `map`, y `collect`.
    
- **`Comparable` y `Comparator` con Lambdas**: Usar lambdas para definir el orden de los elementos en una colección personalizada.