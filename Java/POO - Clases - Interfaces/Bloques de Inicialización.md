```java
class EjemploBloques {
    // Atributo de la clase
    private static int contadorStatic;
    private int contadorInstancia;
    
    // Bloque de inicialización estático (se ejecuta solo una vez al cargar la clase en memoria)
    static {
        System.out.println("Bloque de inicialización estático ejecutado");
        contadorStatic = 100; // Se inicializa el valor de la variable estática
    }
    
    // Bloque de inicialización de instancia (se ejecuta cada vez que se crea un objeto)
    {
        System.out.println("Bloque de inicialización de instancia ejecutado");
        contadorInstancia = 10; // Se inicializa la variable de instancia
    }
    
    // Constructor de la clase
    public EjemploBloques() {
        System.out.println("Constructor ejecutado");
        contadorInstancia += 5; // Modifica el valor después del bloque de inicialización de instancia
    }
    
    // Método para mostrar valores
    public void mostrarValores() {
        System.out.println("contadorStatic: " + contadorStatic);
        System.out.println("contadorInstancia: " + contadorInstancia);
    }
}

public class BloquesInicializacionDemo {
    public static void main(String[] args) {
        System.out.println("Creando primer objeto:");
        EjemploBloques obj1 = new EjemploBloques();
        obj1.mostrarValores();

        System.out.println("\nCreando segundo objeto:");
        EjemploBloques obj2 = new EjemploBloques();
        obj2.mostrarValores();
    }
}

```
