```java
class Persona {
    // Atributos con diferentes niveles de acceso
    public String nombrePublico = "Accesible desde cualquier lugar";
    protected String nombreProtegido = "Accesible dentro del paquete y subclases";
    String nombrePorDefecto = "Accesible solo dentro del paquete"; // Default (sin modificador)
    private String nombrePrivado;
    private int edad;
    
    // Constructor por defecto
    public Persona() {
        this("Nombre por defecto", 0); // Llamada a otro constructor usando this
    }
    
    // Constructor con parámetros
    public Persona(String nombrePrivado) {
        this(nombrePrivado, 0); // Llamada a otro constructor
    }
    
    // Sobrecarga de constructores
    public Persona(String nombrePrivado, int edad) {
        this.nombrePrivado = nombrePrivado;
        this.edad = edad;
    }
    
    // Métodos getter y setter para acceder a atributos privados
    public String getNombrePrivado() {
        return nombrePrivado;
    }
    
    public void setNombrePrivado(String nombrePrivado) {
        this.nombrePrivado = nombrePrivado;
    }
    
    public int getEdad() {
        return edad;
    }
    
    public void setEdad(int edad) {
        this.edad = edad;
    }
    
    // Método para mostrar información
    public void mostrarInfo() {
        System.out.println("Nombre: " + this.nombrePrivado + ", Edad: " + this.edad);
    }
}

public class EncapsulamientoDemo {
    public static void main(String[] args) {
        // Creación de objetos con diferentes constructores
        Persona persona1 = new Persona();
        persona1.mostrarInfo();
        
        Persona persona2 = new Persona("Juan Pérez");
        persona2.mostrarInfo();
        
        Persona persona3 = new Persona("María López", 30);
        persona3.mostrarInfo();
        
        // Modificación del valor privado mediante setter
        persona3.setNombrePrivado("Carlos Gómez");
        persona3.setEdad(35);
        persona3.mostrarInfo();
    }
}
```