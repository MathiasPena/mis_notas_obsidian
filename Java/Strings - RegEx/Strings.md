```java
// Creación de cadenas (String)
String s1 = "Hola Mundo";  // Literal de cadena
String s2 = new String("Hola Mundo"); // Usando el constructor

// Cadenas inmutables: no se pueden modificar después de su creación
// Operaciones con String no modifican el original, crean nuevos objetos

// Concatenación
String s3 = s1 + " y Java"; // Usando el operador '+'
String s4 = s1.concat(" y Java"); // Usando el método concat() (recomendada sobre el '+')

// Comparación de cadenas
boolean isEqual = s1.equals(s2); // Comparar valores de cadenas (case-sensitive)
boolean isEqualIgnoreCase = s1.equalsIgnoreCase(s2); // Ignorar mayúsculas/minúsculas

// Comparar referencias de cadenas
boolean isSameReference = (s1 == s2); // Compara las referencias (no los valores)

// Obtener longitud de una cadena
int length = s1.length(); // Retorna la cantidad de caracteres en la cadena

// Acceder a un carácter en un índice específico
char charAtIndex = s1.charAt(0); // Obtiene el carácter en la posición 0 (H)

// Convertir a minúsculas o mayúsculas
String lowerCase = s1.toLowerCase(); // Convierte a minúsculas
String upperCase = s1.toUpperCase(); // Convierte a mayúsculas

// Reemplazar caracteres o substrings
String replaced = s1.replace("Mundo", "Java"); // Reemplaza "Mundo" por "Java"

// Comprobar si contiene una subcadena
boolean contains = s1.contains("Mundo"); // Verifica si "Mundo" está presente en s1

// Comprobar si la cadena empieza o termina con una subcadena
boolean startsWith = s1.startsWith("Hola"); // Verifica si empieza con "Hola"
boolean endsWith = s1.endsWith("Mundo"); // Verifica si termina con "Mundo"

// Dividir una cadena en un arreglo de subcadenas
String[] splitString = s1.split(" "); // Divide en espacios, obteniendo ["Hola", "Mundo"]

// Obtener una subcadena
String subString = s1.substring(0, 4); // "Hola" (del índice 0 al 4, excluyendo el 4)

// Eliminar espacios al principio y al final
String trimmed = s1.trim(); // Elimina los espacios iniciales y finales

// Comprobar si una cadena es vacía
boolean isEmpty = s1.isEmpty(); // Retorna true si la cadena está vacía

// Conversiones entre tipos y cadena
String numStr = String.valueOf(123); // Convierte un entero a String
int num = Integer.parseInt("123"); // Convierte un String a entero

// Conversión de un array de caracteres a String
char[] charArray = {'H', 'o', 'l', 'a'};
String charArrayToString = new String(charArray); // "Hola"

// Formateo de cadenas
String formatted = String.format("La edad de %s es %d", "Juan", 30); // "La edad de Juan es 30"

// Convertir a String con un delimitador
String joinString = String.join("-", "Java", "is", "fun"); // "Java-is-fun"

// Métodos adicionales
String[] words = s1.split(" "); // "Hola Mundo" -> ["Hola", "Mundo"]
String replacedAll = s1.replaceAll("o", "0"); // Reemplaza todas las 'o' por '0'

// Comparación de cadenas lexicográficamente
int comparison = s1.compareTo(s2); // Devuelve 0 si son iguales, negativo si s1 es menor, positivo si s1 es mayor

// Usando StringBuilder para manipulación eficiente de cadenas
StringBuilder sb = new StringBuilder("Hola");
sb.append(" Mundo"); // Append agrega texto al final
sb.insert(4, " Java "); // Insert inserta en una posición específica
sb.delete(4, 9); // Elimina desde el índice 4 hasta el 9
sb.reverse(); // Invierte la cadena
String result = sb.toString(); // Convierte el StringBuilder en un String normal
```
