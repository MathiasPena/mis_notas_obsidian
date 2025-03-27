```java
public class ThreadInterruptionExample {

    public static void main(String[] args) throws InterruptedException {
        // Crear un hilo que ejecutará una tarea y que puede ser interrumpido
        Thread hilo = new Thread(new MiTareaInterrumpible());
        hilo.start();

        // Dormir durante 2 segundos antes de interrumpir el hilo
        Thread.sleep(2000);
        
        // Interrumpir el hilo después de 2 segundos
        System.out.println("Interrumpiendo el hilo...");
        hilo.interrupt();
        
        // Esperar a que el hilo termine
        hilo.join();
        System.out.println("El hilo ha terminado.");
    }

    // Clase que implementa Runnable para una tarea que puede ser interrumpida
    static class MiTareaInterrumpible implements Runnable {

        @Override
        public void run() {
            try {
                System.out.println("Hilo comenzó a ejecutar. Realizando tarea...");
                
                // Simulación de tarea larga que puede ser interrumpida
                for (int i = 0; i < 10; i++) {
                    // Verifica si el hilo ha sido interrumpido
                    if (Thread.currentThread().isInterrupted()) {
                        System.out.println("El hilo fue interrumpido antes de completar la tarea.");
                        return;
                    }

                    // Simulando trabajo con un sleep
                    Thread.sleep(1000);
                    System.out.println("Tarea " + (i + 1) + " completada.");
                }
            } catch (InterruptedException e) {
                // Manejo de la excepción InterruptedException
                System.out.println("El hilo fue interrumpido durante el sleep.");
                // Reestablecer el estado de interrupción después de capturar la excepción
                Thread.currentThread().interrupt();
            }
        }
    }
}

```

