```java
public class AutoboxingUnboxing {

    public static void main(String[] args) {
        
        // Autoboxing: Conversion automática de primitivo a objeto envoltorio
        int primitivo = 10;
        Integer envoltorio = primitivo;  // Java convierte automáticamente int a Integer (Autoboxing)
        
        System.out.println("Autoboxing: " + envoltorio);
        
        // Unboxing: Conversion automática de objeto envoltorio a primitivo
        Integer envoltorio2 = 20;
        int primitivo2 = envoltorio2;  // Java convierte automáticamente Integer a int (Unboxing)
        
        System.out.println("Unboxing: " + primitivo2);
        
        // Ejemplo con operaciones
        Integer a = 100;  // Autoboxing
        Integer b = 200;  // Autoboxing
        int resultado = a + b;  // Unboxing para realizar la suma
        System.out.println("Resultado de la suma: " + resultado);
        
        // Autoboxing y Unboxing con otros tipos de datos
        Double d = 3.14;  // Autoboxing
        double e = d;  // Unboxing
        System.out.println("Valor double después de Unboxing: " + e);
        
        // Ejemplo con Boolean
        Boolean valor = true;  // Autoboxing
        if (valor) {  // Unboxing implícito
            System.out.println("El valor es verdadero");
        }
        
        // Autoboxing y Unboxing con comparación
        Integer x = 100;
        Integer y = 100;
        if (x == y) {  // Unboxing implícito y comparación
            System.out.println("x e y son iguales después de Unboxing");
        }
        
        // Autoboxing y Unboxing con diferentes valores
        Integer a2 = 500;
        Integer b2 = 500;
        if (a2.equals(b2)) {  // Comparación de objetos, no primitivos
            System.out.println("a2 y b2 son iguales (usando equals())");
        } else {
            System.out.println("a2 y b2 no son iguales (usando equals())");
        }
        
        // Ejemplo con Long
        Long l = 123456789L;  // Autoboxing
        long l2 = l;  // Unboxing
        System.out.println("Long después de Unboxing: " + l2);
    }
}

```
