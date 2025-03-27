```java
// Definición de una clase en Java
class Persona {
    // Atributos de la clase (propiedades o variables de instancia)
    String nombre;
    int edad;
    
    // Constructor sin parámetros (por defecto)
    public Persona() {
        this.nombre = "Desconocido";
        this.edad = 0;
    }
    
    // Constructor con parámetros
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
    
    // Métodos de la clase (comportamientos)
    public void mostrarInfo() {
        System.out.println("Nombre: " + nombre + ", Edad: " + edad);
    }
    
    // Métodos getter y setter
    public String getNombre() {
        return nombre;
    }
    
    public void setNombre(String nombre) {
        this.nombre = nombre;
    }
    
    public int getEdad() {
        return edad;
    }
    
    public void setEdad(int edad) {
        this.edad = edad;
    }
    
    // Método estático
    public static void saludar() {
        System.out.println("Hola, soy una persona!");
    }
    
    // Sobrecarga de método
    public void mostrarInfo(String mensaje) {
        System.out.println(mensaje + " Nombre: " + nombre + ", Edad: " + edad);
    }
}

public class ClasesObjetosDemo {
    public static void main(String[] args) {
        // Creación de objetos (instanciación de la clase)
        Persona persona1 = new Persona(); // Usando constructor sin parámetros
        persona1.mostrarInfo();
        
        Persona persona2 = new Persona("Juan", 25); // Usando constructor con parámetros
        persona2.mostrarInfo();
        
        // Uso de getters y setters
        persona1.setNombre("Ana");
        persona1.setEdad(22);
        System.out.println("Nuevo nombre: " + persona1.getNombre());
        System.out.println("Nueva edad: " + persona1.getEdad());
        
        // Llamada a método estático
        Persona.saludar();
        
        // Sobrecarga de método
        persona2.mostrarInfo("Información: ");
    }
}
```
