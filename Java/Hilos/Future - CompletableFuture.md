```java
import java.util.concurrent.*;

public class FutureAndCompletableFutureExample {

    public static void main(String[] args) {

        // Creando un ExecutorService para manejar las tareas
        ExecutorService executorService = Executors.newFixedThreadPool(2);

        // ---------------------------- Future ----------------------------------

        // Crear una tarea que retorne un resultado (Callable)
        Callable<String> tarea = () -> {
            Thread.sleep(1000); // Simula trabajo
            return "Tarea completada";
        };

        // Enviar la tarea con submit() y obtener un Future
        Future<String> future = executorService.submit(tarea);

        // ------------------- Métodos de Future ------------------

        try {
            // get(): Obtiene el resultado de la tarea. Puede bloquear el hilo hasta que la tarea termine.
            String resultado = future.get(); // Bloquea hasta obtener el resultado
            System.out.println("Resultado de Future: " + resultado);

            // isDone(): Verifica si la tarea ha sido completada (independientemente de si tuvo éxito o falló).
            System.out.println("¿Está la tarea terminada? " + future.isDone());

            // isCancelled(): Verifica si la tarea fue cancelada.
            System.out.println("¿Está la tarea cancelada? " + future.isCancelled());

            // cancel(): Cancela la tarea si aún no ha comenzado a ejecutarse. Devuelve un booleano si fue cancelada con éxito.
            boolean cancelada = future.cancel(true); // true para interrumpir si está en ejecución
            System.out.println("¿Tarea cancelada? " + cancelada);

        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }

        // ------------------ CompletableFuture -------------------

        // Crear una tarea asíncrona con CompletableFuture
        CompletableFuture<String> completableFuture = CompletableFuture.supplyAsync(() -> {
            try {
                Thread.sleep(1000);
                return "Completado en CompletableFuture";
            } catch (InterruptedException e) {
                e.printStackTrace();
                return "Error";
            }
        });

        // ------------------- Métodos de CompletableFuture ---------------------

        // thenApply(): Se ejecuta cuando la tarea inicial se completa con éxito, y puede transformar el resultado.
        completableFuture.thenApply(result -> {
            System.out.println("Resultado transformado: " + result.toUpperCase());
            return result.toUpperCase(); // Retorna un nuevo valor para la cadena
        });

        // thenAccept(): Se ejecuta cuando la tarea inicial se completa con éxito, pero no transforma el resultado.
        completableFuture.thenAccept(result -> {
            System.out.println("Resultado aceptado: " + result);
        });

        // thenRun(): Ejecuta un bloque de código cuando la tarea inicial termine, sin usar el resultado.
        completableFuture.thenRun(() -> {
            System.out.println("La tarea ha terminado, pero no usamos el resultado.");
        });

        // exceptionally(): Maneja errores si la tarea falla, puede usar el resultado por defecto.
        completableFuture.exceptionally(ex -> {
            System.out.println("Error al completar la tarea: " + ex.getMessage());
            return "Valor predeterminado"; // Devuelve un valor por defecto en caso de error
        });

        // allOf(): Espera a que todas las tareas en el arreglo se completen
        CompletableFuture<Void> future1 = CompletableFuture.supplyAsync(() -> {
            try { Thread.sleep(1000); } catch (InterruptedException e) {}
            return "Tarea 1";
        });
        CompletableFuture<Void> future2 = CompletableFuture.supplyAsync(() -> {
            try { Thread.sleep(2000); } catch (InterruptedException e) {}
            return "Tarea 2";
        });
        CompletableFuture<Void> allOf = CompletableFuture.allOf(future1, future2);
        allOf.thenRun(() -> System.out.println("Todas las tareas han finalizado"));

        // anyOf(): Devuelve el resultado de la primera tarea que termine exitosamente
        CompletableFuture<Object> anyOf = CompletableFuture.anyOf(future1, future2);
        anyOf.thenAccept(result -> System.out.println("Primera tarea completada: " + result));

        // -------------------- Métodos adicionales de CompletableFuture ----------------

        // complete(): Completa manualmente el CompletableFuture con un valor
        completableFuture.complete("Completado manualmente");
        completableFuture.thenAccept(result -> System.out.println("Resultado después de completar manualmente: " + result));

        // get(): Similar a Future.get(), bloquea el hilo hasta que el CompletableFuture se complete.
        try {
            String valorFinal = completableFuture.get(); // Bloquea y obtiene el resultado
            System.out.println("Valor final obtenido con get(): " + valorFinal);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }

        // join(): Similar a get(), pero en lugar de lanzar excepciones, se propaga una RuntimeException en caso de error.
        try {
            String valorJoin = completableFuture.join();
            System.out.println("Valor obtenido con join(): " + valorJoin);
        } catch (CompletionException e) {
            System.out.println("Error al usar join(): " + e.getMessage());
        }

        // wait() y notify() para esperar por completar en programación con hilos en Java

        // ------------------- Cerrando el ExecutorService --------------------
        executorService.shutdown(); // Apagar el ExecutorService de manera ordenada
    }
}

```

