## ReentrantLock

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class CuentaBancaria {
    private int saldo = 0;
    private final Lock lock = new ReentrantLock();  // Instanciación de un Lock

    public void depositar(int cantidad) {
        lock.lock();  // Adquirir el lock
        try {
            saldo += cantidad;
            System.out.println("Depositados: " + cantidad + ", Saldo actual: " + saldo);
        } finally {
            lock.unlock();  // Liberar el lock
        }
    }

    public void retirar(int cantidad) {
        lock.lock();  // Adquirir el lock
        try {
            if (cantidad <= saldo) {
                saldo -= cantidad;
                System.out.println("Retirados: " + cantidad + ", Saldo actual: " + saldo);
            } else {
                System.out.println("Fondos insuficientes para retirar " + cantidad);
            }
        } finally {
            lock.unlock();  // Liberar el lock
        }
    }

    public int obtenerSaldo() {
        return saldo;
    }
}

class HiloDeposito extends Thread {
    private CuentaBancaria cuenta;

    public HiloDeposito(CuentaBancaria cuenta) {
        this.cuenta = cuenta;
    }

    @Override
    public void run() {
        cuenta.depositar(100);
    }
}

class HiloRetiro extends Thread {
    private CuentaBancaria cuenta;

    public HiloRetiro(CuentaBancaria cuenta) {
        this.cuenta = cuenta;
    }

    @Override
    public void run() {
        cuenta.retirar(50);
    }
}

public class LocksEjemplo {
    public static void main(String[] args) {
        CuentaBancaria cuenta = new CuentaBancaria();

        // Crear hilos para realizar operaciones de depósito y retiro
        HiloDeposito hiloDeposito = new HiloDeposito(cuenta);
        HiloRetiro hiloRetiro = new HiloRetiro(cuenta);

        // Iniciar los hilos
        hiloDeposito.start();
        hiloRetiro.start();

        try {
            hiloDeposito.join(); // Esperar a que el hilo de depósito termine
            hiloRetiro.join();   // Esperar a que el hilo de retiro termine
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Mostrar el saldo final después de todas las operaciones
        System.out.println("Saldo final: " + cuenta.obtenerSaldo());
    }
}

```

## TryLock

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class CuentaBancaria {
    private int saldo = 0;
    private final Lock lock = new ReentrantLock();

    public void depositar(int cantidad) {
        if (lock.tryLock()) {  // Intentar adquirir el lock
            try {
                saldo += cantidad;
                System.out.println("Depositados: " + cantidad + ", Saldo actual: " + saldo);
            } finally {
                lock.unlock();
            }
        } else {
            System.out.println("No se pudo obtener el lock para depositar.");
        }
    }

    public void retirar(int cantidad) {
        if (lock.tryLock()) {  // Intentar adquirir el lock
            try {
                if (cantidad <= saldo) {
                    saldo -= cantidad;
                    System.out.println("Retirados: " + cantidad + ", Saldo actual: " + saldo);
                } else {
                    System.out.println("Fondos insuficientes para retirar " + cantidad);
                }
            } finally {
                lock.unlock();
            }
        } else {
            System.out.println("No se pudo obtener el lock para retirar.");
        }
    }

    public int obtenerSaldo() {
        return saldo;
    }
}

public class LocksConTryLock {
    public static void main(String[] args) {
        CuentaBancaria cuenta = new CuentaBancaria();

        // Crear hilos para realizar operaciones de depósito y retiro
        Thread hiloDeposito = new Thread(() -> cuenta.depositar(100));
        Thread hiloRetiro = new Thread(() -> cuenta.retirar(50));

        hiloDeposito.start();
        hiloRetiro.start();
    }
}

```

## ReentrantReadWriteLock

```java
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

class RecursoCompartido {
    private int dato = 0;
    private final ReadWriteLock lock = new ReentrantReadWriteLock();

    // Operación de lectura
    public int leer() {
        lock.readLock().lock(); // Adquirir lock de lectura
        try {
            return dato;
        } finally {
            lock.readLock().unlock(); // Liberar lock de lectura
        }
    }

    // Operación de escritura
    public void escribir(int nuevoValor) {
        lock.writeLock().lock(); // Adquirir lock de escritura
        try {
            dato = nuevoValor;
        } finally {
            lock.writeLock().unlock(); // Liberar lock de escritura
        }
    }
}

public class LocksLecturaEscritura {
    public static void main(String[] args) {
        RecursoCompartido recurso = new RecursoCompartido();

        // Hilos de lectura y escritura
        Thread hiloLectura = new Thread(() -> System.out.println("Valor leído: " + recurso.leer()));
        Thread hiloEscritura = new Thread(() -> recurso.escribir(10));

        hiloLectura.start();
        hiloEscritura.start();
    }
}

```

## StampedLock

```java
import java.util.concurrent.locks.StampedLock;

class Recurso {
    private int valor = 0;
    private final StampedLock lock = new StampedLock();

    public int leer() {
        long stamp = lock.readLock();  // Adquirir lock de lectura
        try {
            return valor;
        } finally {
            lock.unlockRead(stamp);  // Liberar lock de lectura
        }
    }

    public void escribir(int nuevoValor) {
        long stamp = lock.writeLock();  // Adquirir lock de escritura
        try {
            valor = nuevoValor;
        } finally {
            lock.unlockWrite(stamp);  // Liberar lock de escritura
        }
    }
}

```

## LockSupport

```java
import java.util.concurrent.locks.LockSupport;

class Recurso {
    private boolean disponible = false;

    public void realizarTarea() {
        System.out.println("Esperando a que el recurso esté disponible...");
        LockSupport.park();  // Suspende el hilo
        if (disponible) {
            System.out.println("Recurso disponible. Tarea completada.");
        } else {
            System.out.println("Recurso aún no disponible.");
        }
    }

    public void liberarRecurso() {
        disponible = true;
        LockSupport.unpark(Thread.currentThread());  // Despierta el hilo suspendido
    }
}

```


