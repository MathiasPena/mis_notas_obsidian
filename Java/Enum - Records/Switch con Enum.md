```java
enum Dia {
    LUNES, MARTES, MIERCOLES, JUEVES, VIERNES, SABADO, DOMINGO;
}

enum Nivel {
    BAJO, MEDIO, ALTO;
}

public class Main {
    public static void main(String[] args) {
        Dia dia = Dia.MARTES;
        Nivel nivel = Nivel.ALTO;

        // Uso de switch con enum
        switch (dia) {
            case LUNES:
                System.out.println("Es lunes, inicio de semana.");
                break;
            case VIERNES:
                System.out.println("Es viernes, casi fin de semana.");
                break;
            case SABADO:
            case DOMINGO:
                System.out.println("Es fin de semana.");
                break;
            default:
                System.out.println("Es un día entre semana.");
        }

        // Uso de switch con otro enum
        switch (nivel) {
            case BAJO -> System.out.println("Nivel bajo.");
            case MEDIO -> System.out.println("Nivel medio.");
            case ALTO -> System.out.println("Nivel alto.");
        }
    }
}

```
