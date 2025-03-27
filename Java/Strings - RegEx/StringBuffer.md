```java
// Crear un StringBuffer
StringBuffer sb1 = new StringBuffer(); // Constructor vacío
StringBuffer sb2 = new StringBuffer("Hola Mundo"); // Constructor con una cadena inicial
StringBuffer sb3 = new StringBuffer(50); // Constructor con capacidad inicial (50 caracteres)

// Métodos de StringBuffer

// Append: Agregar texto al final del StringBuffer
sb1.append("¡Hola "); // Agrega texto al final
sb1.append("Mundo");  // Sigue agregando texto
sb1.append("!");      // Agrega más texto
System.out.println(sb1); // Salida: "¡Hola Mundo!"

// Insert: Insertar texto en una posición específica
sb2.insert(5, "Java "); // Inserta "Java " en el índice 5 de la cadena
System.out.println(sb2); // Salida: "Hola Java Mundo"

// Delete: Eliminar un rango de caracteres
sb2.delete(4, 9); // Elimina los caracteres desde el índice 4 hasta el 9 (sin incluir el 9)
System.out.println(sb2); // Salida: "Hola Mundo"

// Replace: Reemplazar caracteres en un rango
sb2.replace(0, 4, "Adiós"); // Reemplaza los caracteres desde el índice 0 hasta el 4 con "Adiós"
System.out.println(sb2); // Salida: "Adiós Mundo"

// Reverse: Invertir la cadena
sb2.reverse(); // Invierte el contenido del StringBuffer
System.out.println(sb2); // Salida: "odnuM oísdA"

// Capacidad: Capacidad interna del StringBuffer
int capacity = sb2.capacity(); // Devuelve la capacidad actual
System.out.println("Capacidad: " + capacity); // Ejemplo: 32 (depende del tamaño)

// Length: Longitud del StringBuffer
int length = sb2.length(); // Devuelve la cantidad de caracteres actuales
System.out.println("Longitud: " + length); // Ejemplo: 13 (por "odnuM oísdA")

// Obtener carácter en una posición específica
char charAtIndex = sb2.charAt(3); // Obtiene el carácter en el índice 3
System.out.println("Carácter en índice 3: " + charAtIndex); // Ejemplo: "n"

// Convertir StringBuffer a String
String str = sb2.toString(); // Convierte el StringBuffer a un objeto String
System.out.println("String convertido: " + str); // Ejemplo: "odnuM oísdA"

// Establecer una nueva longitud (si es menor, se recorta; si es mayor, se rellena con espacios)
sb2.setLength(10); // Establece la longitud a 10 caracteres
System.out.println(sb2); // Salida: "odnuM oís" (recortado)

// Capacidad de expansión automática
sb1.ensureCapacity(100); // Asegura que el StringBuffer tenga al menos la capacidad especificada (100)
System.out.println("Capacidad después de ensureCapacity(100): " + sb1.capacity()); // Ejemplo: 100

// Trim to size: Ajusta la capacidad para que coincida con la longitud actual
sb2.trimToSize(); // Ajusta la capacidad interna para que sea igual a la longitud
System.out.println("Capacidad después de trimToSize: " + sb2.capacity()); // Ejemplo: 10 (ajustado)

// Substring: Extraer una subcadena
String subStr = sb2.substring(3, 8); // Extrae los caracteres desde el índice 3 hasta el 8 (excluyendo el 8)
System.out.println("Subcadena: " + subStr); // Ejemplo: "nuM o"

// Convertir un array de caracteres a StringBuffer
char[] charArray = {'H', 'o', 'l', 'a'};
StringBuffer sbFromArray = new StringBuffer(new String(charArray)); // Convertir un char[] a StringBuffer
System.out.println(sbFromArray); // Salida: "Hola"
```