
#### ¿Cómo acceder a campos privados y públicos?

La **reflexión** en Java permite acceder y modificar los **campos (atributos)** de una clase en tiempo de ejecución, tanto si son **públicos** como **privados**. Para ello, se usa la clase **`Field`**, que representa un campo de una clase.

- **Campos públicos**: Son accesibles directamente sin restricciones.
    
- **Campos privados**: Aunque no son accesibles directamente, se pueden modificar o leer utilizando reflexión, y para ello es necesario usar **`setAccessible(true)`**.
    

#### Uso de `Field` para obtener y modificar valores de campos dinámicamente

Primero, debes obtener una instancia de la clase `Field` que representa el campo que deseas modificar. Esto se hace utilizando los métodos **`getField()`** y **`getDeclaredField()`**.

- **`getField(String name)`**: Obtiene un campo público especificando su nombre.
    
- **`getDeclaredField(String name)`**: Obtiene cualquier campo (público, privado o protegido) especificando su nombre.
    

Una vez que tienes una instancia de `Field`, puedes usar **`get()`** y **`set()`** para obtener o modificar el valor de ese campo, respectivamente.

- **`get(Object obj)`**: Obtiene el valor de un campo en el objeto especificado.
    
- **`set(Object obj, Object value)`**: Establece el valor de un campo en el objeto especificado.
    

#### Ejemplos de acceder y modificar campos

##### 1. **Acceder y Modificar un Campo Público**

Supongamos que tenemos una clase `Persona` con un campo público:

```java
class Persona {
    public String nombre;

    public Persona(String nombre) {
        this.nombre = nombre;
    }
}
```

Ahora, vamos a acceder y modificar el campo `nombre` utilizando reflexión:

```java
import java.lang.reflect.Field;

public class EjemploReflexion {
    public static void main(String[] args) throws Exception {
        Persona persona = new Persona("Juan");

        // Obtener el campo público 'nombre' de la clase Persona
        Field field = Persona.class.getField("nombre");

        // Obtener el valor del campo en el objeto persona
        String nombre = (String) field.get(persona);
        System.out.println("Nombre original: " + nombre);  // Output: Juan

        // Modificar el valor del campo
        field.set(persona, "Pedro");
        System.out.println("Nombre modificado: " + persona.nombre);  // Output: Pedro
    }
}
```

##### 2. **Acceder y Modificar un Campo Privado**

Ahora supongamos que tenemos un campo privado en la clase `Persona`:

```java
class Persona {
    private int edad;

    public Persona(int edad) {
        this.edad = edad;
    }
}
```

Accedemos y modificamos el campo privado `edad`:

```java
import java.lang.reflect.Field;

public class EjemploReflexion {
    public static void main(String[] args) throws Exception {
        Persona persona = new Persona(25);

        // Obtener el campo privado 'edad' de la clase Persona
        Field field = Persona.class.getDeclaredField("edad");

        // Hacer que el campo privado sea accesible
        field.setAccessible(true);

        // Obtener el valor del campo en el objeto persona
        int edad = (int) field.get(persona);
        System.out.println("Edad original: " + edad);  // Output: 25

        // Modificar el valor del campo
        field.set(persona, 30);
        System.out.println("Edad modificada: " + field.get(persona));  // Output: 30
    }
}
```

##### 3. **Acceder a un Campo Estático**

Si la clase tiene campos estáticos, también puedes acceder a ellos de la misma manera. Ejemplo de un campo estático en la clase `Persona`:

```java
class Persona {
    public static String saludo = "Hola";
}
```

Accediendo al campo estático:

```java
import java.lang.reflect.Field;

public class EjemploReflexion {
    public static void main(String[] args) throws Exception {
        // Obtener el campo estático 'saludo' de la clase Persona
        Field field = Persona.class.getField("saludo");

        // Obtener el valor del campo estático
        String saludo = (String) field.get(null);
        System.out.println("Saludo: " + saludo);  // Output: Hola

        // Modificar el campo estático
        field.set(null, "Hola desde Reflexión");
        System.out.println("Saludo modificado: " + field.get(null));  // Output: Hola desde Reflexión
    }
}
```

### Resumen:

- Usamos la clase **`Field`** para acceder y modificar campos de una clase en tiempo de ejecución.
    
- **`getField()`** y **`getDeclaredField()`** nos permiten acceder a campos públicos y privados, respectivamente.
    
- Los campos privados requieren que usemos **`setAccessible(true)`** para hacerlos accesibles.
    
- Podemos obtener y modificar el valor de los campos usando los métodos **`get()`** y **`set()`**.
    
- La reflexión permite manipular también campos estáticos, pasándolos como `null` al método **`get()`** o **`set()`**.
    

La reflexión es útil para casos donde necesitas trabajar con clases de manera genérica o dinámica, como al crear frameworks o realizar operaciones en tiempo de ejecución que no puedes conocer en tiempo de compilación.