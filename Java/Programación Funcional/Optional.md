```java
import java.util.Optional;

public class OptionalDemo {

    public static void main(String[] args) {

        // Ejemplo 1: Creación de un Optional
        String nombre = "Java";
        Optional<String> optionalNombre = Optional.of(nombre);  // Crea un Optional con valor presente
        System.out.println("Valor del Optional: " + optionalNombre.get());

        // Ejemplo 2: Optional.empty() - Crear un Optional vacío
        Optional<String> optionalVacio = Optional.empty();  // Crea un Optional vacío
        System.out.println("Optional vacío: " + optionalVacio.isPresent());  // false

        // Ejemplo 3: Optional.ofNullable() - Crear un Optional que permite valores nulos
        String apellido = null;
        Optional<String> optionalApellido = Optional.ofNullable(apellido);  // Crea un Optional que puede estar vacío
        System.out.println("¿Apellido presente? " + optionalApellido.isPresent());  // false

        // Ejemplo 4: isPresent() - Verificar si el Optional tiene un valor
        if (optionalNombre.isPresent()) {
            System.out.println("Nombre: " + optionalNombre.get());  // Imprime el valor si está presente
        }

        // Ejemplo 5: ifPresent() - Ejecutar una acción si el valor está presente
        optionalNombre.ifPresent(n -> System.out.println("Nombre usando ifPresent(): " + n));

        // Ejemplo 6: orElse() - Proveer un valor por defecto si el Optional está vacío
        String valorPorDefecto = optionalApellido.orElse("Desconocido");
        System.out.println("Apellido (con valor por defecto): " + valorPorDefecto);

        // Ejemplo 7: orElseGet() - Proveer un valor por defecto usando un proveedor (función lambda)
        String valorPorDefectoConLambda = optionalApellido.orElseGet(() -> "Valor generado");
        System.out.println("Apellido (con valor generado): " + valorPorDefectoConLambda);

        // Ejemplo 8: orElseThrow() - Lanza una excepción si el Optional está vacío
        try {
            String apellidoNoNull = optionalApellido.orElseThrow(() -> new IllegalArgumentException("Apellido es obligatorio"));
        } catch (Exception e) {
            System.out.println("Excepción: " + e.getMessage());
        }

        // Ejemplo 9: map() - Transformar el valor dentro de un Optional (si está presente)
        Optional<String> optionalUpperCase = optionalNombre.map(String::toUpperCase);  // Convierte el valor a mayúsculas si está presente
        System.out.println("Nombre en mayúsculas: " + optionalUpperCase.orElse("Valor nulo"));

        // Ejemplo 10: flatMap() - Similar a map(), pero permite trabajar con un Optional dentro de otro Optional
        Optional<String> optionalConPunto = optionalNombre.flatMap(n -> Optional.of(n + "."));  // Concatenamos un punto si el valor está presente
        System.out.println("Nombre con punto: " + optionalConPunto.orElse("Valor nulo"));

        // Ejemplo 11: filter() - Filtrar el valor dentro de un Optional según una condición
        Optional<String> optionalFiltrado = optionalNombre.filter(n -> n.length() > 3);  // Solo pasa si el nombre tiene más de 3 caracteres
        System.out.println("Nombre filtrado: " + optionalFiltrado.orElse("Valor nulo"));

        // Ejemplo 12: map() y orElse() juntos para un ejemplo más complejo
        Optional<String> resultado = optionalNombre
            .map(n -> "El nombre es: " + n)
            .orElse("Valor no disponible");
        System.out.println("Resultado complejo: " + resultado);

        // Ejemplo 13: Uso de Optional con colecciones y nulls
        Optional<String> itemDeLista = getItemDeLista(null);
        System.out.println("Elemento de lista (null): " + itemDeLista.orElse("Elemento no encontrado"));

        // Ejemplo 14: Uso de Optional con métodos de retorno nulo
        String saludo = getSaludo();
        Optional<String> saludoOpt = Optional.ofNullable(saludo);  // Retorna un Optional con un valor nulo si el saludo es null
        System.out.println("Saludo (Optional): " + saludoOpt.orElse("No se encontró saludo"));

        // Ejemplo 15: Uso de Optional en el contexto de un objeto
        Persona persona = new Persona("Juan", 30);
        Optional<Persona> optionalPersona = Optional.ofNullable(persona);
        System.out.println("Nombre de la persona: " + optionalPersona.map(Persona::getNombre).orElse("Sin nombre"));

        // Ejemplo 16: Filtrando Optional basado en una condición más compleja
        Optional<String> valorFiltrado = Optional.ofNullable("Hola")
            .filter(s -> s.length() > 4);  // Solo pasa si la longitud es mayor que 4
        System.out.println("Valor filtrado: " + valorFiltrado.orElse("Valor no encontrado"));

    }

    // Método que puede retornar un Optional vacío si no encuentra el valor
    public static Optional<String> getItemDeLista(String[] lista) {
        if (lista != null && lista.length > 0) {
            return Optional.of(lista[0]);
        } else {
            return Optional.empty();  // Retorna Optional vacío si no hay elemento
        }
    }

    // Método que retorna un saludo o null si no lo encuentra
    public static String getSaludo() {
        return null;  // Simula un saludo no encontrado
    }

    // Clase Persona usada en el ejemplo 15
    static class Persona {
        private String nombre;
        private int edad;

        public Persona(String nombre, int edad) {
            this.nombre = nombre;
            this.edad = edad;
        }

        public String getNombre() {
            return nombre;
        }

        public int getEdad() {
            return edad;
        }
    }
}

```