```java
// Anotaciones básicas en Java

// @Override: Se usa para indicar que un método sobrescribe un método de la clase padre.
class Animal {
    public void hacerSonido() {
        System.out.println("Animal hace un sonido");
    }
}

class Perro extends Animal {
    @Override
    public void hacerSonido() {
        System.out.println("El perro ladra");
    }
}

// @Deprecated: Se usa para marcar métodos, clases o campos como obsoletos.
class Coche {
    @Deprecated
    public void conducir() {
        System.out.println("Conduciendo un coche antiguo");
    }

    public void conducirNuevo() {
        System.out.println("Conduciendo un coche nuevo");
    }
}

// @SuppressWarnings: Se usa para suprimir advertencias específicas del compilador.
public class Ejemplo {
    @SuppressWarnings("deprecation")
    public static void main(String[] args) {
        Coche coche = new Coche();
        coche.conducir(); // Esto genera una advertencia por el uso de un método marcado como @Deprecated
    }
}

// @FunctionalInterface: Se usa para marcar una interfaz que tiene un solo método abstracto, y así garantizar que se cumpla la característica de función pura.
@FunctionalInterface
interface Operacion {
    int calcular(int a, int b);  // Método abstracto
}

// @SafeVarargs: Indica que el código dentro de un método que usa varargs es seguro para llamar con argumentos de tipo varargs.
class EjemploVarargs {
    @SafeVarargs
    public static <T> void imprimirElementos(T... elementos) {
        for (T elemento : elementos) {
            System.out.println(elemento);
        }
    }
}

// Uso de @Retention y @Target para definir cuándo y dónde se puede usar una anotación.
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.ElementType;
import java.lang.annotation.Target;

// @Retention define si la anotación está disponible en tiempo de compilación o en tiempo de ejecución.
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)  // Indica que esta anotación solo puede usarse en métodos
public @interface MiAnotacion {
    String valor() default "Valor predeterminado";
}

class ClaseConAnotacion {
    @MiAnotacion(valor = "Test")
    public void metodoConAnotacion() {
        System.out.println("Método anotado");
    }
}

```

