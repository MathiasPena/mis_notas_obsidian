 La Stack es la memoria utilizada para almacenar:
    - Llamadas a métodos.
    - Variables locales de cada método.
    - Referencias a objetos en el Heap (pero los objetos en sí están en el Heap).
    - Se crea un "Stack Frame" por cada método llamado y se destruye al finalizar.
    - Es gestionada por cada hilo de manera independiente.
    - Su tamaño es limitado y puede provocar StackOverflowError si se desborda.

```java
class StackExample {
    public static void main(String[] args) {
        System.out.println("Inicio del programa");
        metodoA(); // Se crea un Stack Frame para metodoA()
        System.out.println("Fin del programa");
    }

    static void metodoA() {
        System.out.println("Entrando en metodoA");
        metodoB(); // Se crea un Stack Frame para metodoB()
        System.out.println("Saliendo de metodoA");
    }

    static void metodoB() {
        System.out.println("Ejecutando metodoB");
    }
}

/*
    **Explicación**
    - La Stack empieza con el método `main()`.
    - `main()` llama a `metodoA()`, que crea un nuevo Stack Frame.
    - `metodoA()` llama a `metodoB()`, que crea otro Stack Frame.
    - Cuando `metodoB()` termina, su Stack Frame se elimina.
    - Luego, `metodoA()` termina y su Stack Frame también se elimina.
    - Finalmente, `main()` termina y la Stack se vacía.
*/


// ===================================
// 2. STACK OVERFLOW ERROR
// ===================================

class StackOverflowExample {
    public static void main(String[] args) {
        recursivo(); // Llamada infinita a recursivo()
    }

    static void recursivo() {
        recursivo(); // No hay condición de salida, se sigue llamando a sí mismo
    }
}

/*
    **Explicación**
    - Cada llamada a `recursivo()` crea un nuevo Stack Frame sin eliminar los anteriores.
    - La Stack tiene un tamaño limitado.
    - Cuando se llena, ocurre un **StackOverflowError**.
*/


// ===================================
// 3. VARIABLES LOCALES EN LA STACK
// ===================================

class StackVariablesExample {
    public static void main(String[] args) {
        int x = 10; // `x` se almacena en la Stack
        int y = 20; // `y` también se almacena en la Stack
        sumar(x, y);
    }

    static int sumar(int a, int b) {
        int resultado = a + b; // `resultado` es una variable local en la Stack
        return resultado;
    }
}

/*
    **Explicación**
    - `x` y `y` son variables locales de `main()`, almacenadas en su Stack Frame.
    - `a` y `b` son parámetros locales de `sumar()`, almacenados en el Stack Frame de `sumar()`.
    - `resultado` es otra variable en la Stack de `sumar()`.
    - Cuando `sumar()` termina, su Stack Frame desaparece y sus variables locales también.
*/


// ===================================
// 4. REFERENCIAS A OBJETOS EN STACK
// ===================================

class StackHeapExample {
    public static void main(String[] args) {
        Persona persona1 = new Persona("Carlos"); // `persona1` está en la Stack, pero el objeto está en el Heap
        Persona persona2 = new Persona("Lucía");  // `persona2` es otra referencia en la Stack
        System.out.println(persona1.getNombre());
        System.out.println(persona2.getNombre());
    }
}

class Persona {
    private String nombre;

    public Persona(String nombre) {
        this.nombre = nombre; // `nombre` se almacena en el Heap
    }

    public String getNombre() {
        return nombre;
    }
}

/*
    **Explicación**
    - `persona1` y `persona2` son referencias almacenadas en la Stack de `main()`.
    - Los objetos `Persona` están en el Heap.
    - Cuando `main()` termina, `persona1` y `persona2` desaparecen de la Stack.
    - Los objetos en el Heap solo se eliminan si no hay más referencias a ellos (por el Garbage Collector).
*/


// ===================================
// 5. AJUSTE DEL TAMAÑO DE LA STACK EN JVM
// ===================================

/*
    El tamaño de la Stack se puede ajustar con el flag de JVM:

    -Xss<size>  -> Define el tamaño máximo de la Stack por hilo.

    Ejemplo de ejecución con 512 KB de Stack:
    java -Xss512k StackExample
*/


// ===================================
// CONCLUSIÓN
// ===================================

/*
    RESUMEN DE LA STACK EN JAVA:
    ----------------------------
    - La Stack almacena variables locales, llamadas a métodos y referencias a objetos en el Heap.
    - Cada método tiene su propio **Stack Frame**, que desaparece al terminar la ejecución.
    - Cada hilo tiene su propia Stack independiente.
    - Su tamaño es limitado y puede generar **StackOverflowError** si se llena.
    - Se pueden ajustar sus límites con **-Xss** en la JVM.
```