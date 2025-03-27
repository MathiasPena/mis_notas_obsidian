```java
import java.util.function.Function;

public class FunctionComposition {
    public static void main(String[] args) {
        // Definimos dos funciones lambda
        Function<Integer, Integer> multiplyByTwo = x -> x * 2; // Multiplica por 2
        Function<Integer, Integer> addThree = x -> x + 3; // Suma 3

        // Composición usando andThen():
        // Primero se multiplica por 2, luego se suma 3
        Function<Integer, Integer> multiplyThenAdd = multiplyByTwo.andThen(addThree);
        System.out.println("Resultado de multiplyThenAdd(5): " + multiplyThenAdd.apply(5));  // (5 * 2) + 3 = 13

        // Composición usando compose():
        // Primero se suma 3, luego se multiplica por 2
        Function<Integer, Integer> addThenMultiply = multiplyByTwo.compose(addThree);
        System.out.println("Resultado de addThenMultiply(5): " + addThenMultiply.apply(5));  // (5 + 3) * 2 = 16

        // Composición de más funciones
        Function<Integer, Integer> subtractOne = x -> x - 1; // Resta 1
        Function<Integer, Integer> multiplyThenAddThenSubtract = multiplyByTwo.andThen(addThree).andThen(subtractOne);
        System.out.println("Resultado de multiplyThenAddThenSubtract(5): " + multiplyThenAddThenSubtract.apply(5));  // ((5 * 2) + 3) - 1 = 12
    }
}

```

- **`multiplyByTwo`**: Función que multiplica un número por 2.
    
- **`addThree`**: Función que suma 3 a un número.
    
- **`andThen()`**: Primero aplica la función que está a la izquierda y luego aplica la función que está a la derecha. En el ejemplo `multiplyByTwo.andThen(addThree)`, primero se multiplica por 2 y luego se suma 3.
    
- **`compose()`**: Primero aplica la función que está a la derecha y luego la función que está a la izquierda. En el ejemplo `multiplyByTwo.compose(addThree)`, primero se suma 3 y luego se multiplica por 2.

```scss
Resultado de multiplyThenAdd(5): 13
Resultado de addThenMultiply(5): 16
Resultado de multiplyThenAddThenSubtract(5): 12
```
