
#### Uso de la clase `Class`

En Java, **`Class`** es la clase que representa a las clases en sí mismas. Es a través de `Class` que puedes acceder a información de tiempo de ejecución sobre las clases, como sus métodos, campos, constructores, etc.

Cada clase en Java tiene una instancia única de **`Class`** asociada que proporciona información sobre la clase en tiempo de ejecución.

#### ¿Cómo obtener la clase de un objeto?

Para obtener la clase de un objeto, puedes utilizar el método **`getClass()`**. Este método está disponible para todos los objetos en Java porque provienen de la clase `Object`, que es la superclase de todas las clases en Java.

**Ejemplo:**

```java
String str = "Hola Mundo";
Class<?> clazz = str.getClass();  // Obtiene la clase del objeto str
System.out.println(clazz.getName());  // Output: java.lang.String
```

En este ejemplo, llamamos a `getClass()` en un objeto de tipo `String` y obtenemos la clase asociada con ese objeto, que es `java.lang.String`.

#### ¿Cómo obtener el nombre de la clase, su tipo y otros detalles?

Una vez que tienes una instancia de la clase `Class`, puedes obtener una variedad de detalles sobre la clase, tales como su nombre, los métodos, los campos, los constructores, y más.

- **Nombre de la clase:**
    
    - Usamos `getName()` para obtener el nombre completo de la clase (con su paquete).
        
    
    ```java
    System.out.println(clazz.getName());  // Output: java.lang.String
    ```
    
- **Nombre simple de la clase:**
    
    - `getSimpleName()` devuelve el nombre simple de la clase (sin el paquete).
        
    
    ```java
    System.out.println(clazz.getSimpleName());  // Output: String
    ```
    
- **Tipo de la clase:**
    
    - Usamos `getTypeName()` para obtener el tipo de la clase.
        
    
    ```java
    System.out.println(clazz.getTypeName());  // Output: java.lang.String
    ```
    
- **Superclase:**
    
    - `getSuperclass()` devuelve la superclase directa de la clase.
        
    
    ```java
    Class<?> superClass = clazz.getSuperclass();
    System.out.println(superClass.getName());  // Output: java.lang.Object
    ```
    

#### Ejemplos de obtener clases y objetos en tiempo de ejecución

1. **Obtener la clase de un objeto:**
    
    ```java
    Integer num = 42;
    Class<?> clazz = num.getClass();
    System.out.println(clazz.getName());  // Output: java.lang.Integer
    ```
    
2. **Obtener la clase utilizando `Class.forName()`**: Si conoces el nombre de la clase en forma de cadena, puedes usar **`Class.forName()`** para obtener su instancia.
    
    ```java
    try {
        Class<?> clazz = Class.forName("java.lang.Integer");
        System.out.println(clazz.getName());  // Output: java.lang.Integer
    } catch (ClassNotFoundException e) {
        e.printStackTrace();
    }
    ```
    
3. **Obtener la clase de un tipo primitivo:** Los tipos primitivos también tienen una representación de clase en Java.
    
    ```java
    Class<?> clazz = int.class;
    System.out.println(clazz.getName());  // Output: int
    ```
    
4. **Obtener las clases de las interfaces implementadas:** Un objeto también puede implementar interfaces. Puedes obtenerlas con `getInterfaces()`.
    
    ```java
    Class<?>[] interfaces = clazz.getInterfaces();
    for (Class<?> interfaceClass : interfaces) {
        System.out.println(interfaceClass.getName());  // Output: java.io.Serializable
    }
    ```
    

### Resumen:

- Usamos la clase `Class` para obtener información sobre clases en tiempo de ejecución.
    
- Puedes obtener la clase de un objeto usando **`getClass()`** y detalles sobre la clase como el nombre, superclase, e interfaces.
    
- **`Class.forName()`** permite obtener una clase a partir de su nombre en forma de cadena.
    
- Los tipos primitivos también tienen su representación de clase con la propiedad `class`.
    

La reflexión te permite acceder y manipular información de clases y objetos de manera dinámica, lo que es muy útil para ciertas aplicaciones como frameworks y bibliotecas.