```java
public class TiposEnvoltorio {

    public static void main(String[] args) {

        // Integer (envoltorio para int)
        Integer entero = 42;

        // Double (envoltorio para double)
        Double decimal = 3.1416;

        // Boolean (envoltorio para boolean)
        Boolean esJavaDivertido = true;

        // Character (envoltorio para char)
        Character letra = 'A';

        // Long (envoltorio para long)
        Long numeroLargo = 123456789L;

        // Float (envoltorio para float)
        Float numeroFlotante = 2.718f;

        // Byte (envoltorio para byte)
        Byte numeroPequeno = 127;

        // Short (envoltorio para short)
        Short numeroMediano = 32000;

        // Conversión de primitivo a envoltorio
        int a = 10;
        Integer b = Integer.valueOf(a); // int a Integer

        // Conversión de envoltorio a primitivo
        Integer x = 100;
        int y = x.intValue(); // Integer a int

        // Operaciones con envoltorios
        Integer suma = Integer.valueOf(10).intValue() + Integer.valueOf(20).intValue();
        Double multiplicacion = Double.valueOf(2.5) * Double.valueOf(3.5);

        // Comparación de envoltorios
        Integer num1 = 10;
        Integer num2 = 20;
        boolean sonIguales = num1.equals(num2); // false

        // Uso de métodos estáticos (como parse)
        int parseado = Integer.parseInt("123"); // Convierte String a int
        double parseadoDouble = Double.parseDouble("3.14"); // Convierte String a double

        // Métodos útiles de los envoltorios
        System.out.println("Máximo valor de Integer: " + Integer.MAX_VALUE);
        System.out.println("Mínimo valor de Integer: " + Integer.MIN_VALUE);
        System.out.println("Máximo valor de Double: " + Double.MAX_VALUE);
        System.out.println("Mínimo valor de Double: " + Double.MIN_VALUE);

        // Autoboxing y Unboxing:
        Integer aInteger = 100; // autoboxing: int a Integer
        int aInt = aInteger; // unboxing: Integer a int

        // Ejemplo con Boolean:
        Boolean valorBooleano = true;
        if (valorBooleano) {
            System.out.println("Es verdadero");
        }

        // Ejemplo con Character
        Character caracter = 'A';
        if (Character.isLetter(caracter)) {
            System.out.println(caracter + " es una letra");
        }

        // Ejemplo con métodos de Character:
        char c = '5';
        System.out.println("Es dígito: " + Character.isDigit(c)); // true

        // Métodos de la clase Integer
        Integer max = Integer.max(10, 20);
        System.out.println("Max de 10 y 20: " + max);

        // Otros métodos de Integer
        System.out.println("Valor absoluto de -10: " + Integer.abs(-10));
        System.out.println("Número binario de 10: " + Integer.toBinaryString(10));
        System.out.println("Parseado de '123' a int: " + Integer.parseInt("123"));

        // Métodos de la clase Double
        System.out.println("Valor absoluto de -3.14: " + Math.abs(-3.14));

        // Ejemplo con Long:
        Long largo = Long.valueOf("1234567890");
        System.out.println("Valor de Long: " + largo);

        // Métodos de la clase Float
        Float flotante = 3.14f;
        System.out.println("Número Float: " + flotante);
        
        // Métodos de la clase Short
        Short corto = 32000;
        System.out.println("Valor Short: " + corto);

        // Ejemplo con Byte:
        Byte bte = 127;
        System.out.println("Valor Byte: " + bte);

        // Uso de autoboxing con valores primitivos y objetos
        Integer autoBoxed = 50;  // Java convierte automáticamente de int a Integer
        int unboxed = autoBoxed; // Java convierte automáticamente de Integer a int
        System.out.println("Autoboxing y Unboxing: " + unboxed);

        // Ejemplo con métodos de la clase Boolean
        Boolean val = Boolean.valueOf("true");
        System.out.println("Valor booleano: " + val);
    }
}
```
#### Tipos Envoltorio (Wrapper Classes):

1. **Integer**: Envoltorio para `int`.
    
2. **Double**: Envoltorio para `double`.
    
3. **Boolean**: Envoltorio para `boolean`.
    
4. **Character**: Envoltorio para `char`.
    
5. **Long**: Envoltorio para `long`.
    
6. **Float**: Envoltorio para `float`.
    
7. **Byte**: Envoltorio para `byte`.
    
8. **Short**: Envoltorio para `short`.
    

#### Métodos Comunes:

1. **valueOf()**: Convierte un primitivo en su envoltorio correspondiente (ej. `Integer.valueOf(10)`).
    
2. **intValue(), doubleValue(), longValue()**: Convierte un objeto envoltorio a su tipo primitivo (ej. `Integer.intValue()`).
    
3. **parseInt(), parseDouble()**: Convierte un `String` a su valor numérico primitivo (ej. `Integer.parseInt("10")`).
    
4. **MAX_VALUE y MIN_VALUE**: Devuelven el valor máximo y mínimo de un tipo primitivo correspondiente (ej. `Integer.MAX_VALUE`).
    
5. **toString()**: Devuelve el valor como `String` (ej. `Integer.toString(10)`).
    
6. **compareTo()**: Compara dos objetos envoltorios (ej. `Integer.compareTo()`).
    
7. **equals()**: Compara el contenido de dos objetos envoltorios (ej. `Integer.equals()`).
    
8. **Autoboxing**: Java convierte automáticamente entre primitivos y objetos envoltorios cuando es necesario.
    
9. **Unboxing**: Proceso inverso donde un envoltorio se convierte a su tipo primitivo correspondiente.
    

#### Ejemplos Adicionales:

- **Character**:
    
    - `Character.isLetter()`: Verifica si es una letra.
        
    - `Character.isDigit()`: Verifica si es un dígito.
        
- **Boolean**:
    
    - `Boolean.valueOf("true")`: Convierte un `String` a un valor `Boolean`.
        

#### Autoboxing y Unboxing:

- **Autoboxing**: Conversión automática de un tipo primitivo a su clase envoltorio.
    
- **Unboxing**: Conversión automática de un objeto envoltorio a su tipo primitivo.
    

#### Operaciones Matemáticas:

- Se pueden hacer operaciones matemáticas con tipos envoltorios convirtiéndolos a sus valores primitivos (ej. `intValue()`, `doubleValue()`).
    

#### Otros Métodos:

- `Integer.max()`: Devuelve el valor máximo entre dos enteros.
    
- `Integer.toBinaryString()`: Convierte un número a su representación en binario.
    
- `Character.isLetterOrDigit()`: Verifica si el carácter es una letra o un dígito.
    

### Consideraciones:

- **Eficiencia**: Utilizar tipos envoltorios para operaciones simples puede ser menos eficiente que los tipos primitivos, ya que los objetos requieren más memoria.