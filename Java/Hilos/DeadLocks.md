- **Orden consistente de bloqueo**: Asegurarse de que todos los hilos bloqueen los recursos en el mismo orden.
    
- **Timeouts**: Usar un tiempo de espera para evitar que un hilo espere indefinidamente.
    
- **Evitar anidar bloqueos**: Minimizar la cantidad de recursos bloqueados al mismo tiempo.

```java
// Ejemplo de Deadlock y cómo evitarlo

// Dos clases que representan los recursos que los hilos van a intentar bloquear
class RecursoA {
    public synchronized void metodoA(RecursoB b) {
        System.out.println(Thread.currentThread().getName() + " - bloqueando RecursoA");

        // Simula trabajo
        try { Thread.sleep(100); } catch (InterruptedException e) { e.printStackTrace(); }

        System.out.println(Thread.currentThread().getName() + " - esperando por RecursoB");
        b.metodoB();  // Llamada que provoca el deadlock si es llamado por otro hilo
    }

    public synchronized void metodoA() {
        System.out.println(Thread.currentThread().getName() + " - RecursoA en uso");
    }
}

class RecursoB {
    public synchronized void metodoB(RecursoA a) {
        System.out.println(Thread.currentThread().getName() + " - bloqueando RecursoB");

        // Simula trabajo
        try { Thread.sleep(100); } catch (InterruptedException e) { e.printStackTrace(); }

        System.out.println(Thread.currentThread().getName() + " - esperando por RecursoA");
        a.metodoA();  // Llamada que provoca el deadlock si es llamado por otro hilo
    }

    public synchronized void metodoB() {
        System.out.println(Thread.currentThread().getName() + " - RecursoB en uso");
    }
}

// Simulación del Deadlock
public class DeadlockExample {
    public static void main(String[] args) {
        // Creación de los recursos
        RecursoA recursoA = new RecursoA();
        RecursoB recursoB = new RecursoB();

        // Creación de los hilos
        Thread hilo1 = new Thread(() -> recursoA.metodoA(recursoB), "Hilo-1");
        Thread hilo2 = new Thread(() -> recursoB.metodoB(recursoA), "Hilo-2");

        // Iniciamos los hilos
        hilo1.start();
        hilo2.start();
    }
}

```
