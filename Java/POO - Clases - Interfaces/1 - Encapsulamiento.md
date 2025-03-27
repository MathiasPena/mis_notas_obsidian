```java
class Persona {
    // Atributos con diferentes niveles de acceso
    public String nombrePublico = "Accesible desde cualquier lugar";
    protected String nombreProtegido = "Accesible dentro del paquete y subclases";
    String nombrePorDefecto = "Accesible solo dentro del paquete"; // Default (sin modificador)
    private String nombrePrivado = "Accesible solo dentro de esta clase";
    
    // Constructor
    public Persona(String nombrePrivado) {
        this.nombrePrivado = nombrePrivado;
    }
    
    // Métodos getter y setter para acceder a atributos privados
    public String getNombrePrivado() {
        return nombrePrivado;
    }
    
    public void setNombrePrivado(String nombrePrivado) {
        this.nombrePrivado = nombrePrivado;
    }
}

public class EncapsulamientoDemo {
    public static void main(String[] args) {
        Persona persona = new Persona("Juan Pérez");
        
        // Accediendo a los atributos según su nivel de acceso
        System.out.println(persona.nombrePublico); // Se puede acceder directamente
        System.out.println(persona.nombreProtegido); // Se puede acceder dentro del mismo paquete
        System.out.println(persona.nombrePorDefecto); // Se puede acceder dentro del mismo paquete
        
        // System.out.println(persona.nombrePrivado); // Error: No se puede acceder directamente
        System.out.println(persona.getNombrePrivado()); // Acceso mediante getter
        
        // Modificación del valor privado mediante setter
        persona.setNombrePrivado("María López");
        System.out.println(persona.getNombrePrivado());
    }
}

```