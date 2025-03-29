
#### ¿Cómo acceder a métodos públicos, privados y protegidos?

La **reflexión** en Java te permite acceder a **métodos públicos, privados y protegidos** de una clase en tiempo de ejecución, incluso si no tienes acceso directo a esos métodos en el código fuente. Esto se hace a través de la clase **`Method`**, que representa un método de una clase.

- **Métodos públicos**: Son accesibles directamente sin restricciones.
    
- **Métodos privados y protegidos**: Aunque no son accesibles directamente, se pueden invocar usando la reflexión, modificando la visibilidad mediante **`setAccessible(true)`**.
    

#### Uso de `Method` para invocar métodos dinámicamente

Primero, debes obtener una instancia de la clase `Method`, que se puede obtener de un objeto `Class` usando los métodos **`getMethod()`** o **`getDeclaredMethod()`**. Después, puedes invocar ese método en un objeto mediante **`invoke()`**.

- **`getMethod(String name, Class<?>... parameterTypes)`**: Obtiene un método público, especificando su nombre y los tipos de parámetros.
    
- **`getDeclaredMethod(String name, Class<?>... parameterTypes)`**: Obtiene cualquier método (público, privado o protegido), especificando su nombre y los tipos de parámetros.
    

Una vez que tienes un `Method`, puedes usar **`invoke()`** para invocar el método en un objeto.

#### Ejemplos de invocar métodos con y sin parámetros

##### 1. **Método Público Sin Parámetros**

Supongamos que tenemos una clase `Persona` con un método público sin parámetros:

```java
class Persona {
    public void saludar() {
        System.out.println("Hola!");
    }
}
```

Ahora, vamos a invocar el método **`saludar()`** utilizando reflexión:

```java
import java.lang.reflect.Method;

public class EjemploReflexion {
    public static void main(String[] args) throws Exception {
        Persona persona = new Persona();

        // Obtener el método 'saludar' de la clase Persona
        Method method = Persona.class.getMethod("saludar");

        // Invocar el método sin parámetros en el objeto persona
        method.invoke(persona);  // Output: Hola!
    }
}
```

##### 2. **Método Privado Sin Parámetros**

Supongamos que la clase `Persona` tiene un método privado:

```java
class Persona {
    private void saludarPrivado() {
        System.out.println("Hola desde el método privado!");
    }
}
```

Accedemos al método privado usando **`setAccessible(true)`** para permitir el acceso:

```java
import java.lang.reflect.Method;

public class EjemploReflexion {
    public static void main(String[] args) throws Exception {
        Persona persona = new Persona();

        // Obtener el método privado 'saludarPrivado'
        Method method = Persona.class.getDeclaredMethod("saludarPrivado");

        // Hacer que el método sea accesible
        method.setAccessible(true);

        // Invocar el método sin parámetros en el objeto persona
        method.invoke(persona);  // Output: Hola desde el método privado!
    }
}
```

##### 3. **Método con Parámetros**

Supongamos que la clase `Persona` tiene un método que acepta parámetros:

```java
class Persona {
    public void saludarConNombre(String nombre) {
        System.out.println("Hola, " + nombre + "!");
    }
}
```

Para invocar este método con parámetros, se pasa el valor adecuado a través de **`invoke()`**:

```java
import java.lang.reflect.Method;

public class EjemploReflexion {
    public static void main(String[] args) throws Exception {
        Persona persona = new Persona();

        // Obtener el método 'saludarConNombre' que acepta un parámetro String
        Method method = Persona.class.getMethod("saludarConNombre", String.class);

        // Invocar el método con el parámetro "Juan"
        method.invoke(persona, "Juan");  // Output: Hola, Juan!
    }
}
```

##### 4. **Método con Varios Parámetros**

Supongamos que la clase `Persona` tiene un método que acepta múltiples parámetros:

```java
class Persona {
    public void saludarConDetalles(String nombre, int edad) {
        System.out.println("Hola, " + nombre + ". Tienes " + edad + " años.");
    }
}
```

Para invocar este método con múltiples parámetros:

```java
import java.lang.reflect.Method;

public class EjemploReflexion {
    public static void main(String[] args) throws Exception {
        Persona persona = new Persona();

        // Obtener el método 'saludarConDetalles' que acepta un String y un int
        Method method = Persona.class.getMethod("saludarConDetalles", String.class, int.class);

        // Invocar el método con los parámetros "Juan" y 25
        method.invoke(persona, "Juan", 25);  // Output: Hola, Juan. Tienes 25 años.
    }
}
```

### Resumen:

- La reflexión permite acceder a métodos de una clase, tanto públicos como privados, utilizando la clase **`Method`**.
    
- **`getMethod()`** y **`getDeclaredMethod()`** permiten obtener métodos públicos y privados.
    
- Para invocar un método, usamos **`invoke()`** y pasamos los parámetros adecuados.
    
- La reflexión también permite acceder y modificar métodos privados y protegidos usando **`setAccessible(true)`**.
    
- La invocación de métodos puede realizarse tanto con métodos que no aceptan parámetros como con aquellos que los aceptan, pasando los valores en el orden correcto.
    

La reflexión es una herramienta poderosa que ofrece flexibilidad, pero debe usarse con precaución ya que puede afectar el rendimiento y la seguridad del código.