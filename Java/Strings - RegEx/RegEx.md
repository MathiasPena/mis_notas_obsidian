```java
// Definir una expresión regular (regex) para validar un correo electrónico
String regex = "^[a-zA-Z0-9_+&*-]+(?:\\.[a-zA-Z0-9_+&*-]+)*@(?:[a-zA-Z0-9-]+\\.)+[a-zA-Z]{2,7}$"; // Expresión regular para un correo electrónico válido

// Cadena para probar
String email = "usuario@dominio.com";

// Crear un patrón (Pattern) a partir de la expresión regular
Pattern pattern = Pattern.compile(regex);

// Crear un objeto Matcher para verificar la cadena
Matcher matcher = pattern.matcher(email);

// Verificar si la cadena cumple con la expresión regular
boolean isMatch = matcher.matches(); // Devuelve true si el correo es válido
System.out.println("¿Correo válido? " + isMatch); // Salida: true

// Métodos principales para trabajar con expresiones regulares

// 1. matches() - Verifica si toda la cadena coincide con la expresión regular
boolean result = email.matches(regex); // Devuelve true si la cadena coincide completamente con la regex
System.out.println("¿Correo válido (matches)? " + result); // Salida: true

// 2. find() - Busca una subcadena que coincida con la expresión regular
String text = "Mi número es 12345 y mi código postal es 67890";
Pattern p = Pattern.compile("\\d+"); // Buscar números (\\d+ busca uno o más dígitos)
Matcher m = p.matcher(text);
while (m.find()) {
	System.out.println("Número encontrado: " + m.group()); // Salida: 12345, 67890
}

// 3. replaceAll() - Reemplaza todas las ocurrencias que coincidan con la regex
String modifiedText = text.replaceAll("\\d+", "[NUMERO]"); // Reemplaza los números por "[NUMERO]"
System.out.println(modifiedText); // Salida: Mi número es [NUMERO] y mi código postal es [NUMERO]

// 4. split() - Divide una cadena utilizando una expresión regular como delimitador
String sentence = "apple, banana, cherry, date";
String[] fruits = sentence.split(", "); // Dividir la cadena en base a ", "
for (String fruit : fruits) {
	System.out.println(fruit); // Salida: apple, banana, cherry, date
}

// 5. Pattern.compile() - Compila la expresión regular y la convierte en un patrón (Pattern)
Pattern pattern2 = Pattern.compile("\\d+"); // Buscar números
Matcher matcher2 = pattern2.matcher("abc 123 def 456");
while (matcher2.find()) {
	System.out.println("Número encontrado: " + matcher2.group()); // Salida: 123, 456
}

// 6. group() - Obtiene la subcadena que coincide con la expresión regular
String text2 = "El precio es 250 dólares";
Matcher m2 = Pattern.compile("\\d+").matcher(text2); // Buscar números
while (m2.find()) {
	System.out.println("Precio encontrado: " + m2.group()); // Salida: 250
}

// 7. using metacharacters
String regex2 = "\\d{3}-\\d{2}-\\d{4}"; // Expresión regular para un número de seguro social
String ssn = "123-45-6789";
boolean isValidSSN = ssn.matches(regex2);
System.out.println("¿Número de SSN válido? " + isValidSSN); // Salida: true
```
