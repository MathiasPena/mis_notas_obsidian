```java
class Utilidad {
    // Variable estática compartida entre todas las instancias de la clase
    private static int contadorInstancias = 0;
    
    // Constructor que incrementa el contador cada vez que se crea una instancia
    public Utilidad() {
        contadorInstancias++;
    }
    
    // Método estático que puede ser llamado sin necesidad de instanciar la clase
    public static void mostrarMensaje() {
        System.out.println("Este es un método estático, no necesita una instancia de la clase.");
    }
    
    // Método estático que devuelve el número de instancias creadas
    public static int getContadorInstancias() {
        return contadorInstancias;
    }
    
    // Método de instancia (no estático), necesita una instancia para ser llamado
    public void metodoDeInstancia() {
        System.out.println("Este es un método de instancia, requiere un objeto para ser llamado.");
    }
}

public class StaticDemo {
    public static void main(String[] args) {
        // Llamando al método estático sin crear una instancia
        Utilidad.mostrarMensaje();
        
        // Creando instancias de la clase
        Utilidad obj1 = new Utilidad();
        Utilidad obj2 = new Utilidad();
        Utilidad obj3 = new Utilidad();
        
        // Llamando al método estático para obtener el número de instancias creadas
        System.out.println("Número de instancias creadas: " + Utilidad.getContadorInstancias());
        
        // Intentando llamar a un método de instancia desde una referencia estática (esto dará error si se intenta)
        // Utilidad.metodoDeInstancia(); // ERROR: No se puede llamar a un método de instancia de forma estática
        
        // Llamando a un método de instancia correctamente
        obj1.metodoDeInstancia();
    }
}
```