- **NEW**: El hilo ha sido creado pero aún no ha comenzado a ejecutarse.
    
- **RUNNABLE**: El hilo está listo para ejecutarse, pero puede estar esperando que el procesador le asigne tiempo.
    
- **BLOCKED**: El hilo está esperando obtener acceso a un recurso bloqueado por otro hilo.
    
- **WAITING**: El hilo está esperando indefinidamente a que otro hilo lo notifique para continuar.
    
- **TIMED_WAITING**: El hilo está esperando durante un tiempo específico antes de reanudar.
    
- **TERMINATED**: El hilo ha completado su ejecución.

```java
public class EstadoHilos {

    public static void main(String[] args) throws InterruptedException {

        // Crear un hilo nuevo (estado NEW)
        Thread hilo = new Thread(new MiTarea());
        System.out.println("Estado inicial del hilo: " + hilo.getState()); // NEW

        // Iniciar el hilo
        hilo.start();
        System.out.println("Estado del hilo después de start: " + hilo.getState()); // RUNNABLE (o TIMED_WAITING si entra en sleep)

        // Esperar un momento para que el hilo haga algo
        Thread.sleep(100); // El hilo puede pasar a TIMED_WAITING si está durmiendo
        System.out.println("Estado del hilo después de sleep: " + hilo.getState()); // Puede estar en TIMED_WAITING o RUNNABLE

        // Esperar a que el hilo termine
        hilo.join();
        System.out.println("Estado del hilo después de join: " + hilo.getState()); // TERMINATED
    }
}

class MiTarea implements Runnable {
    @Override
    public void run() {
        try {
            // El hilo estará en TIMED_WAITING mientras duerme
            System.out.println("Hilo en ejecución, estado actual: " + Thread.currentThread().getState()); // RUNNABLE
            Thread.sleep(500); // El hilo entra en TIMED_WAITING
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

```
