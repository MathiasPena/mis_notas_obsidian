```java
public class DaemonThreads {

    public static void main(String[] args) throws InterruptedException {
        // Crear un hilo no daemon
        Thread hiloNormal = new Thread(new MiTarea(), "Hilo Normal");
        hiloNormal.start();

        // Crear un hilo daemon
        Thread hiloDaemon = new Thread(new MiTarea(), "Hilo Daemon");
        hiloDaemon.setDaemon(true);  // Configurar el hilo como daemon
        hiloDaemon.start();

        // Mostrar los estados de los hilos
        System.out.println("Estado del Hilo Normal: " + hiloNormal.getState()); // RUNNABLE
        System.out.println("Estado del Hilo Daemon: " + hiloDaemon.getState()); // RUNNABLE

        // Esperar a que el hilo normal termine (el daemon no bloquea la salida)
        hiloNormal.join();

        // Al terminar el hilo principal, el hilo daemon se detendrá, aunque aún esté ejecutando
        System.out.println("Hilo principal ha terminado. Hilo daemon puede seguir ejecutándose, pero no lo impide.");
    }

    // Clase que implementa Runnable, usada para los hilos
    static class MiTarea implements Runnable {
        @Override
        public void run() {
            // Ejemplo de tarea que simula trabajo en segundo plano
            for (int i = 0; i < 5; i++) {
                try {
                    System.out.println(Thread.currentThread().getName() + " trabajando... Iteración " + (i + 1));
                    Thread.sleep(1000); // Simular trabajo de 1 segundo
                } catch (InterruptedException e) {
                    System.out.println(Thread.currentThread().getName() + " fue interrumpido");
                }
            }
        }
    }
}

```
