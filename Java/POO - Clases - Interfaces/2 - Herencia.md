```java
// Clase base o superclase
class Persona {
    protected String nombre;
    protected int edad;
    
    // Constructor de la superclase
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
    
    // Método para mostrar información
    public void mostrarInfo() {
        System.out.println("Nombre: " + nombre + ", Edad: " + edad);
    }
}

// Clase derivada o subclase (Hereda de Persona)
class Estudiante extends Persona {
    private String carrera;
    
    // Constructor de la subclase que usa super para llamar al constructor de la superclase
    public Estudiante(String nombre, int edad, String carrera) {
        super(nombre, edad); // Llamada al constructor de Persona
        this.carrera = carrera;
    }
    
    // Método adicional de la subclase
    @Override
    public void mostrarInfo() {
        super.mostrarInfo(); // Llamada al método de la superclase
        System.out.println("Carrera: " + carrera);
    }
}

// Clase derivada adicional (Ejemplo de herencia múltiple indirecta)
class EstudianteDeportista extends Estudiante {
    private String deporte;
    
    public EstudianteDeportista(String nombre, int edad, String carrera, String deporte) {
        super(nombre, edad, carrera);
        this.deporte = deporte;
    }
    
    // Sobrescritura del método mostrarInfo
    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        System.out.println("Deporte: " + deporte);
    }
}

// Interfaz para agregar funcionalidad adicional
interface Becado {
    void mostrarBeca();
}

// Clase que implementa una interfaz
class EstudianteBecado extends Estudiante implements Becado {
    private String tipoBeca;
    
    public EstudianteBecado(String nombre, int edad, String carrera, String tipoBeca) {
        super(nombre, edad, carrera);
        this.tipoBeca = tipoBeca;
    }
    
    @Override
    public void mostrarBeca() {
        System.out.println("Tipo de beca: " + tipoBeca);
    }
    
    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        mostrarBeca();
    }
}

// Clase abstracta con método abstracto
abstract class Trabajador {
    protected String empresa;
    
    public Trabajador(String empresa) {
        this.empresa = empresa;
    }
    
    // Método abstracto que debe ser implementado por las subclases
    public abstract void trabajar();
}

// Clase que extiende una clase abstracta y hereda de otra clase
class EstudianteTrabajador extends Estudiante implements Becado {
    private String trabajo;
    private String tipoBeca;
    
    public EstudianteTrabajador(String nombre, int edad, String carrera, String trabajo, String tipoBeca) {
        super(nombre, edad, carrera);
        this.trabajo = trabajo;
        this.tipoBeca = tipoBeca;
    }
    
    @Override
    public void trabajar() {
        System.out.println(nombre + " trabaja en: " + trabajo);
    }
    
    @Override
    public void mostrarBeca() {
        System.out.println("Tipo de beca: " + tipoBeca);
    }
    
    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        trabajar();
        mostrarBeca();
    }
}

public class HerenciaDemo {
    public static void main(String[] args) {
        // Creación de un objeto de la subclase
        Estudiante estudiante = new Estudiante("Juan", 20, "Ingeniería");
        estudiante.mostrarInfo();

        System.out.println();
        
        // Creación de un objeto de una subclase más específica
        EstudianteDeportista estudianteDeportista = new EstudianteDeportista("María", 22, "Medicina", "Natación");
        estudianteDeportista.mostrarInfo();
        
        System.out.println();
        
        // Creación de un objeto que implementa una interfaz
        EstudianteBecado estudianteBecado = new EstudianteBecado("Carlos", 23, "Derecho", "Académica");
        estudianteBecado.mostrarInfo();
        
        System.out.println();
        
        // Creación de un objeto que hereda e implementa una interfaz
        EstudianteTrabajador estudianteTrabajador = new EstudianteTrabajador("Ana", 25, "Arquitectura", "Estudio de diseño", "Deportiva");
        estudianteTrabajador.mostrarInfo();
    }
}
```
