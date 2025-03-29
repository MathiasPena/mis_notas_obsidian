```java
// Definición básica de un enum
enum Dia {
    LUNES, MARTES, MIERCOLES, JUEVES, VIERNES, SABADO, DOMINGO;
}

// Enum con atributos y métodos
enum Nivel {
    BAJO(1), MEDIO(2), ALTO(3);
    
    private final int valor;

    Nivel(int valor) {
        this.valor = valor;
    }

    public int getValor() {
        return valor;
    }

    public static Nivel getPorValor(int valor) {
        for (Nivel n : values()) {
            if (n.getValor() == valor) {
                return n;
            }
        }
        return null;
    }
}

// Métodos disponibles en un enum
enum Estado {
    ACTIVO, INACTIVO, SUSPENDIDO;

    // Método personalizado en enum
    public void imprimirEstado() {
        System.out.println("El estado actual es: " + this);
    }
}

public class Main {
    public static void main(String[] args) {
        // Uso básico
        Dia dia = Dia.LUNES;
        System.out.println(dia); // LUNES

        // Métodos en enums
        System.out.println(Dia.valueOf("MARTES")); // MARTES
        System.out.println(Dia.values().length); // 7
        for (Dia d : Dia.values()) {
            System.out.println(d.name() + " en posición " + d.ordinal());
        }

        // Uso de un enum con atributos y métodos
        Nivel nivel = Nivel.ALTO;
        System.out.println(nivel.getValor()); // 3
        System.out.println(Nivel.getPorValor(2)); // MEDIO

        // Uso de método personalizado en enum
        Estado estado = Estado.ACTIVO;
        estado.imprimirEstado(); // "El estado actual es: ACTIVO"
    }
}

```