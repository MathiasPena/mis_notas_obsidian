
## ExecutorService con Callable

```java
import java.util.concurrent.*;

class Tarea implements Callable<Integer> {
    private final int num;

    public Tarea(int num) {
        this.num = num;
    }

    @Override
    public Integer call() throws Exception {
        System.out.println("Hilo ejecutando tarea: " + num);
        return num * num;  // Retorna el cuadrado del número
    }
}

public class ExecutorServiceDemo {
    public static void main(String[] args) {
        // Crear un pool de hilos con 2 hilos
        ExecutorService executor = Executors.newFixedThreadPool(2);

        // Crear 3 tareas para ejecutar
        Callable<Integer> tarea1 = new Tarea(2);
        Callable<Integer> tarea2 = new Tarea(3);
        Callable<Integer> tarea3 = new Tarea(4);

        // Ejecutar las tareas y obtener los resultados
        try {
            // Submit devuelve un Future que puede ser usado para obtener el resultado
            Future<Integer> resultado1 = executor.submit(tarea1);
            Future<Integer> resultado2 = executor.submit(tarea2);
            Future<Integer> resultado3 = executor.submit(tarea3);

            // Obtener el resultado de cada tarea
            System.out.println("Resultado tarea 1: " + resultado1.get());  // Espera a que termine y obtiene el resultado
            System.out.println("Resultado tarea 2: " + resultado2.get());
            System.out.println("Resultado tarea 3: " + resultado3.get());
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            // Cerrar el ExecutorService
            executor.shutdown();
        }
    }
}

```

## Metodos

```java
import java.util.concurrent.*;
import java.util.List;

public class ExecutorServiceExample {
    public static void main(String[] args) {
        
        // Crear un pool de hilos con 3 hilos
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Crear tareas usando Callable
        Callable<String> tarea1 = () -> {
            Thread.sleep(1000);
            return "Tarea 1 completada";
        };
        Callable<String> tarea2 = () -> {
            Thread.sleep(2000);
            return "Tarea 2 completada";
        };
        Callable<String> tarea3 = () -> {
            Thread.sleep(500);
            return "Tarea 3 completada";
        };

        // Métodos de ExecutorService
        try {
            // 1. submit(): Enviar una tarea y obtener un Future
            Future<String> resultado1 = executor.submit(tarea1); // Devuelve un Future
            Future<String> resultado2 = executor.submit(tarea2);
            System.out.println("Resultado tarea 1: " + resultado1.get()); // Esperar y obtener el resultado

            // 2. invokeAll(): Ejecuta todas las tareas y espera que todas terminen
            List<Callable<String>> tareas = List.of(tarea1, tarea2, tarea3);
            List<Future<String>> resultados = executor.invokeAll(tareas); // Ejecuta todas las tareas y devuelve los resultados

            // Imprimir todos los resultados
            for (Future<String> resultado : resultados) {
                System.out.println("Resultado tarea: " + resultado.get()); // Obtener resultados de todas las tareas
            }

            // 3. invokeAny(): Ejecuta todas las tareas y devuelve el resultado de la primera que termine
            String resultadoFinal = executor.invokeAny(tareas); // Devuelve el resultado de la primera tarea que termina
            System.out.println("Resultado de la primera tarea completada: " + resultadoFinal);

            // 4. shutdown(): Cierra el ExecutorService de forma ordenada
            executor.shutdown(); // Detiene el executor de manera ordenada, no aceptará nuevas tareas

            // 5. shutdownNow(): Detiene todas las tareas inmediatamente
            List<Runnable> tareasPendientes = executor.shutdownNow(); // Intenta detener las tareas y retorna las que están pendientes
            System.out.println("Tareas pendientes: " + tareasPendientes.size());

            // 6. isShutdown(): Verifica si el ExecutorService está cerrado
            System.out.println("¿Está el Executor cerrado? " + executor.isShutdown());

            // 7. isTerminated(): Verifica si todas las tareas han terminado
            System.out.println("¿Todas las tareas han terminado? " + executor.isTerminated());
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            // 8. awaitTermination(): Espera que todas las tareas finalicen o se interrumpan
            try {
                if (!executor.awaitTermination(60, TimeUnit.SECONDS)) {
                    System.out.println("Tiempo de espera agotado, cerrando las tareas restantes.");
                }
            } catch (InterruptedException e) {
                System.out.println("Error en el tiempo de espera de cierre.");
                Thread.currentThread().interrupt();
            }
        }
    }
}

```

## Con múltiples tareas concurrentes

```java
import java.util.concurrent.*;

public class ExecutorServiceMultipleTasks {
    public static void main(String[] args) {
        // Crear un pool de hilos con 3 hilos
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Crear varias tareas
        Callable<String> tarea1 = () -> {
            Thread.sleep(1000);
            return "Tarea 1 completada";
        };
        Callable<String> tarea2 = () -> {
            Thread.sleep(2000);
            return "Tarea 2 completada";
        };
        Callable<String> tarea3 = () -> {
            Thread.sleep(1500);
            return "Tarea 3 completada";
        };

        // Enviar las tareas al executor
        try {
            // Se ejecutan las tareas concurrentemente
            List<Callable<String>> tareas = List.of(tarea1, tarea2, tarea3);
            List<Future<String>> resultados = executor.invokeAll(tareas);  // Ejecuta todas las tareas

            // Imprimir los resultados
            for (Future<String> resultado : resultados) {
                System.out.println(resultado.get());  // Imprime el resultado de cada tarea
            }
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            // Cerrar el ExecutorService
            executor.shutdown();
        }
    }
}

```

