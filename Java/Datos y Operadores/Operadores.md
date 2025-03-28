```java
public class Operadores {

    public static void main(String[] args) {
        
        // Operadores Aritméticos
        int a = 10;
        int b = 5;
        
        int suma = a + b;      // Suma
        int resta = a - b;     // Resta
        int multiplicacion = a * b;  // Multiplicación
        int division = a / b;  // División
        int modulo = a % b;    // Módulo (resto de la división)
        
        System.out.println("Suma: " + suma);
        System.out.println("Resta: " + resta);
        System.out.println("Multiplicación: " + multiplicacion);
        System.out.println("División: " + division);
        System.out.println("Módulo: " + modulo);
        
        // Operadores Relacionales
        boolean igual = (a == b);     // Igualdad
        boolean diferente = (a != b); // Diferencia
        boolean mayor = (a > b);      // Mayor que
        boolean menor = (a < b);      // Menor que
        boolean mayorIgual = (a >= b); // Mayor o igual
        boolean menorIgual = (a <= b); // Menor o igual
        
        System.out.println("a == b: " + igual);
        System.out.println("a != b: " + diferente);
        System.out.println("a > b: " + mayor);
        System.out.println("a < b: " + menor);
        System.out.println("a >= b: " + mayorIgual);
        System.out.println("a <= b: " + menorIgual);
        
        // Operadores Lógicos
        boolean x = true;
        boolean y = false;
        
        boolean and = (x && y);    // AND lógico
        boolean or = (x || y);     // OR lógico
        boolean not = !x;          // NOT lógico
        
        System.out.println("x && y: " + and);
        System.out.println("x || y: " + or);
        System.out.println("!x: " + not);
        
        // Operadores de Asignación
        int c = 5;
        c += 3;  // Suma con asignación
        c -= 2;  // Resta con asignación
        c *= 4;  // Multiplicación con asignación
        c /= 2;  // División con asignación
        c %= 3;  // Módulo con asignación
        
        System.out.println("c después de operaciones de asignación: " + c);
        
        // Operadores de Incremento y Decremento
        int d = 10;
        
        int preIncremento = ++d; // Incremento antes de usar la variable
        int postIncremento = d++; // Incremento después de usar la variable
        
        int preDecremento = --d; // Decremento antes de usar la variable
        int postDecremento = d--; // Decremento después de usar la variable
        
        System.out.println("Pre incremento: " + preIncremento);
        System.out.println("Post incremento: " + postIncremento);
        System.out.println("Pre decremento: " + preDecremento);
        System.out.println("Post decremento: " + postDecremento);
        
        // Operadores Condicionales (Ternarios)
        int max = (a > b) ? a : b;  // Si a es mayor que b, asigna a, sino asigna b
        System.out.println("El valor máximo es: " + max);
        
        // Operadores de Tipo
        Object obj = "Texto";
        boolean esString = obj instanceof String;  // Verifica el tipo de un objeto
        System.out.println("obj es una instancia de String: " + esString);
    }
}
```
