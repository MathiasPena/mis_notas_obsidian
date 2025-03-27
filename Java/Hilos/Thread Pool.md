```java
import java.util.concurrent.*;

public class ThreadPoolExample {

    public static void main(String[] args) throws InterruptedException {
        // Crear un pool de hilos con un número fijo de hilos (tamaño 2)
        ExecutorService fixedThreadPool = Executors.newFixedThreadPool(2);
        System.out.println("Usando Fixed Thread Pool");

        // Enviar tareas al thread pool
        for (int i = 0; i < 5; i++) {
            fixedThreadPool.submit(new MiTarea(i));
        }

        // Cerrar el pool después de terminar las tareas
        fixedThreadPool.shutdown();
        while (!fixedThreadPool.isTerminated()) {
            // Esperamos a que terminen todas las tareas
        }
        System.out.println("Todas las tareas han terminado en Fixed Thread Pool.");

        // Crear un pool de hilos con número variable de hilos (se crea un hilo por cada tarea)
        ExecutorService cachedThreadPool = Executors.newCachedThreadPool();
        System.out.println("Usando Cached Thread Pool");

        // Enviar tareas al thread pool
        for (int i = 0; i < 5; i++) {
            cachedThreadPool.submit(new MiTarea(i));
        }

        // Cerrar el pool después de terminar las tareas
        cachedThreadPool.shutdown();
        while (!cachedThreadPool.isTerminated()) {
            // Esperamos a que terminen todas las tareas
        }
        System.out.println("Todas las tareas han terminado en Cached Thread Pool.");

        // Crear un pool de hilos con un solo hilo (se ejecuta una tarea a la vez)
        ExecutorService singleThreadExecutor = Executors.newSingleThreadExecutor();
        System.out.println("Usando Single Thread Executor");

        // Enviar tareas al thread pool
        for (int i = 0; i < 5; i++) {
            singleThreadExecutor.submit(new MiTarea(i));
        }

        // Cerrar el pool después de terminar las tareas
        singleThreadExecutor.shutdown();
        while (!singleThreadExecutor.isTerminated()) {
            // Esperamos a que terminen todas las tareas
        }
        System.out.println("Todas las tareas han terminado en Single Thread Executor.");
    }

    // Clase que implementa Runnable, usada para las tareas en los hilos
    static class MiTarea implements Runnable {
        private final int tareaId;

        public MiTarea(int tareaId) {
            this.tareaId = tareaId;
        }

        @Override
        public void run() {
            try {
                System.out.println("Ejecutando tarea " + tareaId + " en " + Thread.currentThread().getName());
                Thread.sleep(1000); // Simulamos una tarea que toma tiempo
            } catch (InterruptedException e) {
                System.out.println("Tarea " + tareaId + " interrumpida");
            }
        }
    }
}

```

