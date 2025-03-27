## Thread

```java
// Ejemplo de creación de hilo utilizando la clase Thread

class MiHilo extends Thread {
    @Override
    public void run() {
        // Código que se ejecutará en el hilo
        for (int i = 0; i < 5; i++) {
            System.out.println("Hilo " + Thread.currentThread().getId() + ": Iteración " + i);
            try {
                Thread.sleep(1000); // Pausa de 1 segundo
            } catch (InterruptedException e) {
                System.out.println("Hilo interrumpido");
            }
        }
    }

    public static void main(String[] args) {
        MiHilo hilo1 = new MiHilo();
        hilo1.start(); // Inicia el hilo

        MiHilo hilo2 = new MiHilo();
        hilo2.start(); // Inicia otro hilo
    }
}

```

## Thread Metodos

```java
class HiloDeEjemplo extends Thread {

    @Override
    public void run() {
        System.out.println("Hilo iniciado: " + getName());

        try {
            // Pausar el hilo por 2 segundos
            sleep(2000);
            System.out.println("Hilo despertado: " + getName());
        } catch (InterruptedException e) {
            System.out.println("Hilo interrumpido: " + getName());
        }

        for (int i = 0; i < 5; i++) {
            System.out.println(getName() + " - Iteración " + i);
            try {
                sleep(1000); // Pausa de 1 segundo
            } catch (InterruptedException e) {
                System.out.println(getName() + " interrumpido");
            }
        }

        System.out.println(getName() + " terminado");
    }

    public static void main(String[] args) throws InterruptedException {
        HiloDeEjemplo hilo1 = new HiloDeEjemplo();
        hilo1.setName("Hilo-1");
        hilo1.setPriority(Thread.MAX_PRIORITY); // Establecer máxima prioridad
        hilo1.start(); // Inicia el hilo

        // Esperar que hilo1 termine
        hilo1.join();

        // Verificar si el hilo está vivo
        System.out.println("¿Está vivo hilo1? " + hilo1.isAlive());

        // Crear otro hilo
        HiloDeEjemplo hilo2 = new HiloDeEjemplo();
        hilo2.setName("Hilo-2");
        hilo2.setPriority(Thread.MIN_PRIORITY); // Establecer mínima prioridad
        hilo2.start(); // Inicia el hilo

        // Obtener el ID y el nombre del hilo
        System.out.println("ID de hilo2: " + hilo2.getId());
        System.out.println("Nombre de hilo2: " + hilo2.getName());

        // Esperar que hilo2 termine
        hilo2.join();

        // Verificar el estado de los hilos
        System.out.println("Estado de hilo1: " + hilo1.getState());
        System.out.println("Estado de hilo2: " + hilo2.getState());

        // Interrumpir hilo2
        hilo2.interrupt();
        System.out.println("¿Hilo2 interrumpido? " + hilo2.isInterrupted());
    }
}

```

## Runnable


```java
// Ejemplo de creación de hilo utilizando Runnable

class MiRunnable implements Runnable {
    @Override
    public void run() {
        // Código que se ejecutará en el hilo
        for (int i = 0; i < 5; i++) {
            System.out.println("Hilo " + Thread.currentThread().getId() + ": Iteración " + i);
            try {
                Thread.sleep(1000); // Pausa de 1 segundo
            } catch (InterruptedException e) {
                System.out.println("Hilo interrumpido");
            }
        }
    }

    public static void main(String[] args) {
        MiRunnable tarea = new MiRunnable();
        Thread hilo1 = new Thread(tarea); // Crear un hilo con Runnable
        hilo1.start(); // Inicia el hilo

        Thread hilo2 = new Thread(tarea); // Crear otro hilo con el mismo Runnable
        hilo2.start(); // Inicia otro hilo
    }
}

```

## Runnable - Lambda

```java
// Ejemplo de creación de hilo utilizando un Lambda con Runnable

public class HilosConLambda {
    public static void main(String[] args) {
        // Creación de hilo con un Lambda para Runnable
        Runnable tarea = () -> {
            for (int i = 0; i < 5; i++) {
                System.out.println("Hilo " + Thread.currentThread().getId() + ": Iteración " + i);
                try {
                    Thread.sleep(1000); // Pausa de 1 segundo
                } catch (InterruptedException e) {
                    System.out.println("Hilo interrumpido");
                }
            }
        };

        // Crear y ejecutar hilos con Runnable
        Thread hilo1 = new Thread(tarea);
        hilo1.start();

        Thread hilo2 = new Thread(tarea);
        hilo2.start();
    }
}

```

## Thread.sleep()

```java
// Ejemplo usando Thread.sleep()

class HiloConSleep extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Hilo con sleep: Iteración " + i);
            try {
                Thread.sleep(1000); // Pausa de 1 segundo entre iteraciones
            } catch (InterruptedException e) {
                System.out.println("Hilo interrumpido");
            }
        }
    }

    public static void main(String[] args) {
        HiloConSleep hilo = new HiloConSleep();
        hilo.start(); // Inicia el hilo
    }
}

```

## Thread.join()

```java
// Ejemplo usando Thread.join()

class HiloConJoin extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Hilo: Iteración " + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                System.out.println("Hilo interrumpido");
            }
        }
    }

    public static void main(String[] args) throws InterruptedException {
        HiloConJoin hilo1 = new HiloConJoin();
        hilo1.start(); // Inicia el hilo
        
        hilo1.join(); // Espera a que hilo1 termine antes de continuar
        
        System.out.println("Hilo principal continúa después de que hilo1 termine");
    }
}

```

## Hilos en Paralelo

```java
// Ejemplo con diferentes tareas en hilos

class Tarea1 implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Tarea 1 - Hilo: Iteración " + i);
            try {
                Thread.sleep(1000); // Pausa de 1 segundo
            } catch (InterruptedException e) {
                System.out.println("Tarea 1 interrumpida");
            }
        }
    }
}

class Tarea2 implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Tarea 2 - Hilo: Iteración " + i);
            try {
                Thread.sleep(500); // Pausa más corta
            } catch (InterruptedException e) {
                System.out.println("Tarea 2 interrumpida");
            }
        }
    }
}

public class HilosConDiferentesTareas {
    public static void main(String[] args) {
        // Crear y ejecutar los hilos con tareas diferentes
        Thread hilo1 = new Thread(new Tarea1());
        hilo1.start();

        Thread hilo2 = new Thread(new Tarea2());
        hilo2.start();
    }
}

```
