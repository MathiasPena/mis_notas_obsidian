```java
class CuentaBancaria {
    private int saldo = 0;

    // Método sincronizado para garantizar que solo un hilo pueda modificar el saldo a la vez
    public synchronized void depositar(int cantidad) {
        saldo += cantidad;
        System.out.println("Depositados: " + cantidad + ", Saldo actual: " + saldo);
    }

    // Método sincronizado para garantizar que solo un hilo pueda modificar el saldo a la vez
    public synchronized void retirar(int cantidad) {
        if (cantidad <= saldo) {
            saldo -= cantidad;
            System.out.println("Retirados: " + cantidad + ", Saldo actual: " + saldo);
        } else {
            System.out.println("Fondos insuficientes para retirar " + cantidad);
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
        // Depósito de dinero en la cuenta
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
        // Intento de retiro de dinero
        cuenta.retirar(50);
    }
}

public class SincronizacionEjemplo {
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