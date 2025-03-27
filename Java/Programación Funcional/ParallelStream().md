```java
import java.util.Arrays;
import java.util.List;

public class ParallelStreamExample {
    public static void main(String[] args) {
        // Lista de números
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Usando parallelStream() para procesar en paralelo
        int sum = numbers.parallelStream()
                         .mapToInt(Integer::intValue)  // Convertir Integer a int
                         .sum();                       // Sumar todos los elementos

        System.out.println("Suma de los números usando parallelStream(): " + sum);

        // Otro ejemplo con operaciones de filtrado y transformación
        List<String> words = Arrays.asList("apple", "banana", "cherry", "date", "elderberry");

        // Procesando la lista de palabras en paralelo: convertir a mayúsculas y contar palabras con más de 5 letras
        long count = words.parallelStream()
                          .map(String::toUpperCase)          // Convertir a mayúsculas
                          .filter(word -> word.length() > 5)  // Filtrar palabras con más de 5 letras
                          .count();                          // Contar las palabras resultantes

        System.out.println("Cantidad de palabras con más de 5 letras en paralelo: " + count);
    }
}

```

