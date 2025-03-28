```java
public class TiposDeDatosPrimitivos {

    public static void main(String[] args) {
        
        // int (entero)
        int numeroEntero = 42;

        // double (número decimal)
        double numeroDecimal = 3.1416;

        // char (carácter)
        char letra = 'A';

        // boolean (verdadero o falso)
        boolean esJavaDivertido = true;

        // long (número entero más grande)
        long numeroLargo = 123456789L; // 'L' indica que es un valor long

        // float (número decimal con menos precisión)
        float numeroFlotante = 2.718f; // 'f' indica que es un valor float

        // byte (número pequeño)
        byte numeroPequeno = 127;

        // short (número entero de tamaño intermedio)
        short numeroMediano = 32000;
        
        // Conversión implícita de tipos numéricos
        int a = 5;
        double b = a; // int se convierte automáticamente a double
        
        // Conversión explícita de tipos numéricos (casting)
        double c = 5.7;
        int d = (int) c; // Conversión explícita de double a int

        // Operaciones con tipos primitivos
        int suma = 10 + 20;
        double division = 10.0 / 3.0;
        char nuevoCarácter = (char)(letra + 1); // Incrementar el valor ASCII
        boolean comparacion = numeroEntero > 30;

        // Operadores unarios
        int x = 5;
        int y = ++x; // Incremento antes de la asignación

        // Operadores de asignación
        int z = 10;
        z += 5; // z = z + 5

        // Operadores ternarios
        int resultado = (x > y) ? x : y; // Si x es mayor que y, toma x; de lo contrario, toma y

        // Ejemplo de tipo booleano
        boolean respuesta = (10 > 5); // Comparación que devuelve true

        // Uso de char con operaciones aritméticas
        char letra1 = 'A';
        char letra2 = (char)(letra1 + 1); // Incrementar el valor ASCII de A

        // Ejemplo con char y concatenación
        char char1 = 'H';
        char char2 = 'i';
    }
}

```

