```java
class Calculadora {

    // Método para sumar dos enteros
    public int sumar(int a, int b) {
        return a + b;
    }

    // Método sobrecargado para sumar tres enteros
    public int sumar(int a, int b, int c) {
        return a + b + c;
    }

    // Método sobrecargado para sumar dos números decimales
    public double sumar(double a, double b) {
        return a + b;
    }
    
    // Método sobrecargado para sumar un entero y un decimal
    public double sumar(int a, double b) {
        return a + b;
    }

    public static void main(String[] args) {
        Calculadora calc = new Calculadora();
        
        // Llamadas a los métodos sobrecargados
        System.out.println("Suma de dos enteros: " + calc.sumar(5, 3));        // 8
        System.out.println("Suma de tres enteros: " + calc.sumar(5, 3, 2));    // 10
        System.out.println("Suma de dos decimales: " + calc.sumar(5.5, 3.3));  // 8.8
        System.out.println("Suma de entero y decimal: " + calc.sumar(5, 3.5)); // 8.5
    }
}

```
