```java
import java.util.*;
import java.util.stream.*;
import java.util.function.*;
import java.util.function.Function;

public class CollectorsExample {
    public static void main(String[] args) {
        // Ejemplo de Collectors.toList()
        List<String> nombres = Arrays.asList("Juan", "Ana", "Carlos", "Pedro", "María");

        // Usamos Collectors.toList() para recolectar los resultados en una lista
        List<String> nombresList = nombres.stream()
                                          .filter(nombre -> nombre.startsWith("J"))
                                          .collect(Collectors.toList()); // Filtra nombres que empiezan con "J"

        System.out.println("Nombres con 'J': " + nombresList);

        // Ejemplo de Collectors.joining()
        // Unimos los elementos en un String con un delimitador
        String nombresString = nombres.stream()
                                      .collect(Collectors.joining(", ", "[", "]"));

        System.out.println("Nombres unidos: " + nombresString);  // Salida: [Juan, Ana, Carlos, Pedro, María]

        // Ejemplo de Collectors.groupingBy()
        // Agrupamos los nombres por la primera letra
        Map<Character, List<String>> nombresPorLetra = nombres.stream()
                                                              .collect(Collectors.groupingBy(nombre -> nombre.charAt(0)));

        System.out.println("Nombres agrupados por letra inicial: " + nombresPorLetra);

        // Ejemplo de Collectors.counting()
        // Contamos cuántos nombres empiezan con la letra "P"
        long count = nombres.stream()
                            .filter(nombre -> nombre.startsWith("P"))
                            .collect(Collectors.counting());

        System.out.println("Cantidad de nombres que comienzan con 'P': " + count);  // Salida: 1

        // Ejemplo de Collectors.mapping()
        // Aplicamos una transformación a los elementos y luego los recolectamos
        List<String> longitudes = nombres.stream()
                                         .collect(Collectors.mapping(String::toUpperCase, Collectors.toList()));

        System.out.println("Nombres en mayúsculas: " + longitudes);

        // Ejemplo de Collectors.partitioningBy()
        // Dividimos los nombres en dos grupos: uno con los que tienen más de 4 letras y otro con menos o igual a 4
        Map<Boolean, List<String>> particion = nombres.stream()
                                                     .collect(Collectors.partitioningBy(nombre -> nombre.length() > 4));

        System.out.println("Partición por longitud: " + particion);

        // Ejemplo de Collectors.toMap()
        // Creamos un mapa con el nombre como clave y su longitud como valor
        Map<String, Integer> nombresAMedidas = nombres.stream()
                                                     .collect(Collectors.toMap(Function.identity(), String::length));

        System.out.println("Mapa de nombres y su longitud: " + nombresAMedidas);
    }
}

```

