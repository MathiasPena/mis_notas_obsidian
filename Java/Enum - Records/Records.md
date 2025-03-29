```java
// Definición de un record
record Persona(String nombre, int edad) {}

// Uso básico
public class Main {
    public static void main(String[] args) {
        Persona p = new Persona("Juan", 30);
        System.out.println(p.nombre()); // Acceso directo a los atributos
        System.out.println(p.edad());

        // toString(), equals() y hashCode() generados automáticamente
        System.out.println(p);
        Persona p2 = new Persona("Juan", 30);
        System.out.println(p.equals(p2)); // true (mismo contenido)
        System.out.println(p.hashCode()); // Código hash generado basado en los atributos
    }
}

// Record con métodos adicionales
record Producto(String nombre, double precio) {
    public double precioConIVA() {
        return precio * 1.21;
    }
}

// Record con constructor personalizado y validación
record Usuario(String nombre, String email) {
    public Usuario {
        if (nombre == null || nombre.isBlank()) throw new IllegalArgumentException("Nombre no puede estar vacío");
        if (!email.contains("@")) throw new IllegalArgumentException("Email inválido");
    }
}

// Record anidado dentro de una clase
class Orden {
    record Item(String producto, int cantidad) {}
}

// Implementando una interfaz en un record
interface Identificable {
    String getId();
}

record Cliente(String id, String nombre) implements Identificable {
    @Override
    public String getId() {
        return id;
    }
}

// Record con constructor compacto (sin repetir campos)
record Punto(int x, int y) {
    public Punto {
        System.out.println("Creando Punto: (" + x + ", " + y + ")");
    }
}

// Uso de record en un switch
record Estado(String nombre) {}

public class MainSwitch {
    public static void main(String[] args) {
        Estado e = new Estado("activo");

        switch (e.nombre()) {
            case "activo" -> System.out.println("El estado es activo");
            case "inactivo" -> System.out.println("El estado es inactivo");
            default -> System.out.println("Estado desconocido");
        }
    }
}

```

### **Puntos clave sobre `record` en Java**

✔ **Son inmutables**: No permiten modificar sus atributos después de la creación.  
✔ **Menos código**: Generan automáticamente `getters`, `equals()`, `hashCode()`, y `toString()`.  
✔ **Ideales para DTOs**: Usados en APIs para transferir datos de forma eficiente.  
✔ **Más eficientes**: Consumen menos memoria y tienen mejor rendimiento que clases normales.  
✔ **No admiten herencia**: No pueden extender otras clases, pero sí implementar interfaces.  
✔ **Solo almacenan datos**: No son adecuados si necesitas lógica de negocio dentro de la clase.

📌 **Ejemplo:**

```java
public record UserDTO(Long id, String nombre, String email) {}
```

📌 **Uso en API con Spring Boot:**

```java
@GetMapping("/{id}")
public ResponseEntity<UserDTO> getUsuario(@PathVariable Long id) {
    return ResponseEntity.ok(new UserDTO(id, "Mathias", "mathias@email.com"));
}
```

✅ **Cada request genera un nuevo objeto sin modificar los existentes.**