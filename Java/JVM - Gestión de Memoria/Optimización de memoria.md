## **1. Uso Eficiente del Heap**

El **Heap** es el área de memoria donde la JVM almacena objetos. Para optimizar su uso:

✅ **Evita objetos innecesarios:** No crees objetos dentro de bucles si puedes reutilizarlos.  
✅ **Usa `StringBuilder` en vez de `String` cuando sea mutable:**

```java

// MAL: Se crean múltiples objetos String en el Heap
String texto = "";
for (int i = 0; i < 1000; i++) {
    texto += i; // Cada concatenación crea un nuevo objeto
}

// BIEN: Usa StringBuilder para evitar objetos innecesarios
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);
}
String textoOptimizado = sb.toString(); // Solo un objeto final
```

✅ **Evita Autoboxing innecesario:** Prefiere **primitivos** sobre `Integer`, `Double`, etc.

```java
// MAL: Se crean muchos objetos innecesarios
List<Integer> lista = new ArrayList<>();
for (int i = 0; i < 1000; i++) {
    lista.add(i); // Cada `i` se convierte en un objeto `Integer`
}

// BIEN: Usa primitivos cuando sea posible
int[] array = new int[1000];
for (int i = 0; i < 1000; i++) {
    array[i] = i; // Sin objetos innecesarios
}
```

✅ **Usa `static` para constantes compartidas:**

```java
class Config {
    static final String APP_NAME = "MiApp"; // Solo un objeto en memoria
}
```

---

## **2. Recolección de Basura (Garbage Collection)**

✅ **Evita memory leaks con estructuras de datos grandes** (ejemplo: listas con referencias innecesarias).

```java
List<Object> lista = new ArrayList<>();
lista.add(new Object()); // Si no se limpia, la memoria se llena

lista.clear(); // Libera referencias
System.gc();   // Sugerimos limpiar memoria
```

✅ **Usa referencias débiles (`WeakReference`) en cachés:**

```java
import java.lang.ref.WeakReference;

Object obj = new Object();
WeakReference<Object> weakRef = new WeakReference<>(obj);

obj = null;
System.gc(); // Si no hay referencias fuertes, el objeto será eliminado

System.out.println(weakRef.get()); // Probablemente sea null
```

---

## **3. Optimización del Stack y Evitar Desbordamiento (Stack Overflow)**

✅ **Evita recursión profunda sin control:**

```java
// MAL: Puede causar StackOverflowError
public int factorial(int n) {
    return n == 0 ? 1 : n * factorial(n - 1);
}

// BIEN: Usa recursión con cola (tail recursion) o iteración
public int factorialOptimizado(int n) {
    int resultado = 1;
    for (int i = 1; i <= n; i++) {
        resultado *= i;
    }
    return resultado;
}
```

✅ **No abuses de las variables locales dentro de métodos grandes.**

---

## **4. Pooling de Objetos (Reutilización en Lugar de Creación)**

✅ **Usa pools de conexiones en bases de datos:**

```java
// Usa un DataSource en vez de abrir conexiones directamente
DataSource ds = new HikariDataSource();
Connection conn = ds.getConnection(); // Reutiliza conexiones
```

✅ **Usa `ThreadPoolExecutor` en vez de crear nuevos threads:**

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
executor.submit(() -> System.out.println("Tarea ejecutada"));
executor.shutdown();
```

✅ **Usa `Integer.valueOf()` en vez de `new Integer()`:**

```java
Integer a = Integer.valueOf(127); // Usa el pool de Integer (-128 a 127)
Integer b = Integer.valueOf(127);
System.out.println(a == b); // true, misma referencia en memoria
```

---

## **5. Uso de Estructuras de Datos Adecuadas**

✅ **Usa `ArrayList` en lugar de `LinkedList` cuando haya muchas búsquedas:**

```java
List<Integer> lista = new ArrayList<>(); // Búsqueda rápida por índice (O(1))
```

✅ **Usa `LinkedList` si hay muchas inserciones/eliminaciones en el medio:**

```java
List<Integer> lista = new LinkedList<>(); // Eliminaciones eficientes (O(1))
```

✅ **Usa `HashMap` en lugar de `TreeMap` si no necesitas ordenación:**

```java
Map<String, Integer> mapa = new HashMap<>(); // Búsquedas rápidas (O(1))
```

✅ **Usa `EnumSet` en vez de `HashSet` para conjuntos pequeños de valores constantes:**

```java
enum Dias {LUNES, MARTES, MIERCOLES}
EnumSet<Dias> diasLaborables = EnumSet.of(Dias.LUNES, Dias.MARTES);
```

---

## **6. Strings y Optimización de Memoria**

✅ **Usa `intern()` para evitar duplicados en el Pool de Strings:**

```java
String s1 = "Hola";
String s2 = new String("Hola").intern(); // Apunta al mismo objeto en el pool
System.out.println(s1 == s2); // true
```

✅ **Evita concatenaciones dentro de bucles con `+`, usa `StringBuilder`:**

```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);
}
```

---

## **7. Configuración de la JVM para Optimización**

✅ **Ajusta el tamaño del Heap según la aplicación:**

```bash
java -Xms512m -Xmx2g MiApp
```

✅ **Usa `-XX:+UseG1GC` para mejorar el rendimiento del GC:**

```bash
java -XX:+UseG1GC -Xms512m -Xmx2g MiApp
```

✅ **Monitorea la memoria con herramientas como `jvisualvm` y `jconsole`.**

---

## **RESUMEN GENERAL**

📌 **Buenas prácticas para optimizar memoria en Java:**

1. **Evita la creación innecesaria de objetos.**
    
2. **Usa referencias débiles (`WeakReference`, `SoftReference`) en cachés.**
    
3. **Reutiliza objetos con pooling (`ThreadPoolExecutor`, `Integer.valueOf()`).**
    
4. **Selecciona la estructura de datos correcta (`ArrayList`, `HashMap`, `EnumSet`).**
    
5. **Configura la JVM adecuadamente (`-Xms`, `-Xmx`, `-XX:+UseG1GC`).**
    
6. **Evita recursión profunda y optimiza el uso del Stack.**
    
7. **Monitorea la memoria con `jvisualvm` y `jconsole`.**
    
8. **Usa `StringBuilder` en lugar de `String` en bucles.**
    
9. **Cierra recursos (`try-with-resources`) para evitar memory leaks.**
    
10. **Evita autoboxing y prefiere tipos primitivos cuando sea posible.**