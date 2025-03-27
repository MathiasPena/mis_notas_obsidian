```java
import java.util.*;
import java.util.stream.*;
import java.util.function.*;

public class StreamAPI {

    public static void main(String[] args) {

        // Lista de ejemplo para trabajar con Stream
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
        
        // 1. Crear un Stream desde una lista
        Stream<Integer> stream = numeros.stream();

        // 2. Filtrar elementos usando filter()
        List<Integer> pares = numeros.stream()
                                      .filter(n -> n % 2 == 0)  // Filtra números pares
                                      .collect(Collectors.toList());
        System.out.println("Números pares: " + pares);

        // 3. Mapear elementos usando map()
        List<Integer> cuadrados = numeros.stream()
                                         .map(n -> n * n)  // Calcula el cuadrado de cada número
                                         .collect(Collectors.toList());
        System.out.println("Cuadrados: " + cuadrados);

        // 4. Reducción usando reduce()
        Optional<Integer> suma = numeros.stream()
                                        .reduce((a, b) -> a + b);  // Suma de todos los números
        System.out.println("Suma total: " + suma.orElse(0));

        // 5. Buscar un elemento usando findFirst() o findAny()
        Optional<Integer> primerPar = numeros.stream()
                                             .filter(n -> n % 2 == 0)
                                             .findFirst();  // Encuentra el primer número par
        System.out.println("Primer número par: " + primerPar.orElse(-1));

        // 6. Comprobación con allMatch(), anyMatch() y noneMatch()
        boolean todosPares = numeros.stream()
                                    .allMatch(n -> n % 2 == 0);  // Verifica si todos los números son pares
        System.out.println("¿Todos los números son pares? " + todosPares);

        boolean algunPar = numeros.stream()
                                  .anyMatch(n -> n % 2 == 0);  // Verifica si al menos uno es par
        System.out.println("¿Hay algún número par? " + algunPar);

        boolean ningunPar = numeros.stream()
                                   .noneMatch(n -> n % 2 == 0);  // Verifica si no hay ningún número par
        System.out.println("¿No hay números pares? " + ningunPar);

        // 7. Ordenar elementos con sorted()
        List<Integer> ordenados = numeros.stream()
                                         .sorted()  // Ordena de menor a mayor
                                         .collect(Collectors.toList());
        System.out.println("Números ordenados: " + ordenados);

        // Ordenar en orden descendente
        List<Integer> ordenadosDescendentes = numeros.stream()
                                                     .sorted(Comparator.reverseOrder())  // Orden descendente
                                                     .collect(Collectors.toList());
        System.out.println("Números ordenados de forma descendente: " + ordenadosDescendentes);

        // 8. Uso de limit() para obtener una cantidad limitada de elementos
        List<Integer> primerosTres = numeros.stream()
                                            .limit(3)  // Toma los primeros 3 números
                                            .collect(Collectors.toList());
        System.out.println("Primeros tres números: " + primerosTres);

        // 9. Saltar elementos usando skip()
        List<Integer> sinPrimerosTres = numeros.stream()
                                               .skip(3)  // Salta los primeros 3 números
                                               .collect(Collectors.toList());
        System.out.println("Sin los tres primeros números: " + sinPrimerosTres);

        // 10. Transformar una lista a un Set utilizando collect()
        Set<Integer> numerosUnicos = numeros.stream()
                                            .collect(Collectors.toSet());  // Convierte la lista en un Set
        System.out.println("Conjunto de números únicos: " + numerosUnicos);

        // 11. Contar el número de elementos con count()
        long cantidadPares = numeros.stream()
                                    .filter(n -> n % 2 == 0)  // Filtra números pares
                                    .count();  // Cuenta la cantidad de números pares
        System.out.println("Cantidad de números pares: " + cantidadPares);

        // 12. Agrupar elementos usando collect() y GroupingBy
        Map<Integer, List<Integer>> agrupadosPorParidad = numeros.stream()
                                                                 .collect(Collectors.groupingBy(n -> n % 2));  // Agrupa por paridad (0 para pares, 1 para impares)
        System.out.println("Agrupados por paridad: " + agrupadosPorParidad);

        // 13. Concatenar strings con collect() y joining()
        List<String> palabras = Arrays.asList("Java", "Stream", "API");
        String concatenado = palabras.stream()
                                     .collect(Collectors.joining(", "));  // Concatena las palabras con una coma
        System.out.println("Palabras concatenadas: " + concatenado);

        // 14. Transformación a un mapa con Collectors.toMap()
        Map<Integer, String> mapa = palabras.stream()
                                            .collect(Collectors.toMap(String::length, Function.identity()));  // Mapea la longitud de las palabras a las palabras mismas
        System.out.println("Mapa de palabras por longitud: " + mapa);

        // 15. Uso de peek() para depuración intermedia
        List<Integer> depurado = numeros.stream()
                                        .peek(n -> System.out.println("Depurando: " + n))  // Imprime cada número mientras se procesa
                                        .collect(Collectors.toList());

        // 16. Conversiones entre Stream y colecciones
        // Convertir Stream a lista
        List<Integer> listaDeStream = numeros.stream()
                                             .collect(Collectors.toList());
        System.out.println("Lista de Stream: " + listaDeStream);

        // Convertir Stream a conjunto
        Set<Integer> setDeStream = numeros.stream()
                                          .collect(Collectors.toSet());
        System.out.println("Set de Stream: " + setDeStream);

        // 17. Uso de forEach() para imprimir elementos
        numeros.stream().forEach(n -> System.out.println("Elemento: " + n));

        // 18. Uso de parallelStream() para procesamiento paralelo
        List<Integer> resultadosParalelos = numeros.parallelStream()
                                                   .map(n -> n * 2)  // Multiplica cada número por 2 en paralelo
                                                   .collect(Collectors.toList());
        System.out.println("Resultados de procesamiento paralelo: " + resultadosParalelos);
    }
}

```

