```java
// Ejemplo completo de uso de ThreadLocal

// ThreadLocal se utiliza para crear variables que son específicas de cada hilo
public class ThreadLocalExample {

    // Declaramos una variable ThreadLocal
    private static ThreadLocal<Integer> threadLocalValue = ThreadLocal.withInitial(() -> 0);

    // Clase que simula un hilo que utiliza la variable ThreadLocal
    static class MyThread extends Thread {
        @Override
        public void run() {
            // Asignamos un valor específico para este hilo
            threadLocalValue.set((int) (Math.random() * 100));

            // Mostramos el valor local del hilo
            System.out.println(Thread.currentThread().getName() + " - Valor de ThreadLocal: " + threadLocalValue.get());
        }
    }

    public static void main(String[] args) throws InterruptedException {
        // Creación de varios hilos
        Thread thread1 = new MyThread();
        Thread thread2 = new MyThread();
        Thread thread3 = new MyThread();

        // Iniciamos los hilos
        thread1.start();
        thread2.start();
        thread3.start();

        // Esperamos a que los hilos terminen
        thread1.join();
        thread2.join();
        thread3.join();

        // Verificamos que los valores de ThreadLocal son independientes por hilo
        System.out.println("Valor final de ThreadLocal en el hilo principal: " + threadLocalValue.get());

        // Limpiar el valor de ThreadLocal, esto es opcional, ya que se limpia automáticamente al finalizar el hilo
        threadLocalValue.remove();
    }
}

```
