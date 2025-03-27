```java
import java.util.*;
import java.util.function.*;

// Ejemplos de funciones anónimas en Java

public class FuncionesAnonimas {

    public static void main(String[] args) {

        // 1. Función anónima utilizando la interfaz Runnable
        Runnable tarea = new Runnable() {
            @Override
            public void run() {
                System.out.println("Tarea ejecutada en un hilo.");
            }
        };
        // Ejecutamos la tarea en un hilo
        Thread hilo = new Thread(tarea);
        hilo.start();

        // 2. Función anónima usando interfaz Comparator para ordenar una lista de cadenas
        List<String> nombres = Arrays.asList("Ana", "Juan", "Carlos", "Pedro");

        // Ordenar de forma descendente usando función anónima
        Collections.sort(nombres, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return o2.compareTo(o1);  // Comparación en orden inverso
            }
        });
        System.out.println("Lista ordenada (descendente): " + nombres);

        // 3. Función anónima usando la interfaz Predicate
        Predicate<Integer> esPar = new Predicate<Integer>() {
            @Override
            public boolean test(Integer t) {
                return t % 2 == 0;  // Verifica si un número es par
            }
        };
        System.out.println("¿Es 4 par?: " + esPar.test(4)); // true

        // 4. Función anónima utilizando Function para convertir String a Integer
        Function<String, Integer> convertir = new Function<String, Integer>() {
            @Override
            public Integer apply(String s) {
                return Integer.parseInt(s);  // Convierte String a Integer
            }
        };
        System.out.println("Conversión de '123' a Integer: " + convertir.apply("123")); // 123

        // 5. Uso de Consumer para procesar una lista sin devolver nada
        List<String> lista = Arrays.asList("Apple", "Banana", "Cherry");
        Consumer<String> mostrarElemento = new Consumer<String>() {
            @Override
            public void accept(String s) {
                System.out.println(s);  // Imprime cada elemento
            }
        };
        lista.forEach(mostrarElemento);

        // 6. Función anónima para mapear valores en una lista con la interfaz Function
        List<String> palabras = Arrays.asList("java", "python", "javascript");

        // Convertir cada palabra a mayúsculas
        List<String> mayusculas = new ArrayList<>();
        for (String palabra : palabras) {
            mayusculas.add(new Function<String, String>() {
                @Override
                public String apply(String t) {
                    return t.toUpperCase();
                }
            }.apply(palabra));
        }
        System.out.println("Palabras en mayúsculas: " + mayusculas);

        // 7. Uso de Runnable para ejecutar una tarea periódicamente
        Runnable tareaPeriodica = new Runnable() {
            @Override
            public void run() {
                System.out.println("Tarea periódica ejecutada.");
            }
        };
        // Ejecutamos la tarea en un hilo
        Timer timer = new Timer();
        timer.scheduleAtFixedRate(new TimerTask() {
            @Override
            public void run() {
                tareaPeriodica.run();
            }
        }, 0, 2000); // Ejecuta cada 2 segundos

        // 8. Uso de Interface funcional con un método (Función anónima)
        interface Saludo {
            void decirSaludo(String mensaje);
        }

        Saludo saludo = new Saludo() {
            @Override
            public void decirSaludo(String mensaje) {
                System.out.println("Saludo: " + mensaje);
            }
        };
        saludo.decirSaludo("¡Hola mundo!");

        // 9. Uso de Iterator con función anónima para recorrer una lista
        Iterator<Integer> iterator = Arrays.asList(1, 2, 3, 4, 5).iterator();
        while (iterator.hasNext()) {
            Integer numero = iterator.next();
            new Consumer<Integer>() {
                @Override
                public void accept(Integer n) {
                    System.out.println("Número: " + n);  // Imprime cada número
                }
            }.accept(numero);
        }

        // 10. Función anónima como argumento para métodos
        List<Integer> numeros = Arrays.asList(10, 20, 30, 40);
        int resultado = realizarOperacion(numeros, new UnaryOperator<Integer>() {
            @Override
            public Integer apply(Integer t) {
                return t * 2; // Multiplicamos por 2
            }
        });
        System.out.println("Resultado de la operación: " + resultado); // Resultado: 200
    }

    // Método que acepta una función anónima como argumento
    public static int realizarOperacion(List<Integer> lista, UnaryOperator<Integer> operador) {
        int suma = 0;
        for (Integer numero : lista) {
            suma += operador.apply(numero);  // Aplica la operación a cada número
        }
        return suma;
    }
}

```

