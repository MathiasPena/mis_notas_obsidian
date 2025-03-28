```java
// TIPOS PRIMITIVOS

int intValue = 10;
double doubleValue = 20.5;
boolean booleanValue = true;
char charValue = 'a';
long longValue = 100L;
short shortValue = 5;

// TIPOS ENVOLVENTE Y SUS MÉTODOS

// Integer (envoltorio de int)
Integer x = 10;
Integer y = 20;
System.out.println(x.intValue());  // Retorna el valor int
System.out.println(x.compareTo(y)); // Compara dos Integer
System.out.println(Integer.sum(x, y)); // Suma dos enteros
System.out.println(Integer.parseInt("123")); // Convierte un String a int
System.out.println(Integer.valueOf("100"));  // Convierte un String a Integer
System.out.println(Integer.toBinaryString(x)); // Convierte a cadena binaria
System.out.println(Integer.toHexString(x));    // Convierte a cadena hexadecimal

// Double (envoltorio de double)
Double a = 10.5;
Double b = 20.5;
System.out.println(a.doubleValue());    // Retorna el valor double
System.out.println(a.compareTo(b));     // Compara dos Double
System.out.println(Double.sum(a, b));   // Suma dos doubles
System.out.println(Double.parseDouble("123.45")); // Convierte un String a double
System.out.println(Double.valueOf("100.5")); // Convierte un String a Double
System.out.println(Double.toString(a)); // Convierte a String

// Boolean (envoltorio de boolean)
Boolean t = true;
Boolean f = false;
System.out.println(t.booleanValue());  // Retorna el valor booleano
System.out.println(Boolean.parseBoolean("true")); // Convierte un String a booleano
System.out.println(Boolean.valueOf("false"));     // Convierte un String a Boolean
System.out.println(Boolean.toString(t)); // Convierte a String

// Character (envoltorio de char)
Character c = 'a';
System.out.println(c.charValue());    // Retorna el valor char
System.out.println(Character.isDigit(c)); // Verifica si es un dígito
System.out.println(Character.isLetter(c)); // Verifica si es una letra
System.out.println(Character.toLowerCase(c)); // Convierte a minúscula
System.out.println(Character.toUpperCase(c)); // Convierte a mayúscula

// Long (envoltorio de long)
Long l = 100L;
Long m = 200L;
System.out.println(l.longValue());    // Retorna el valor long
System.out.println(l.compareTo(m));   // Compara dos Long
System.out.println(Long.parseLong("12345")); // Convierte un String a long
System.out.println(Long.valueOf("100000"));  // Convierte un String a Long

// Short (envoltorio de short)
Short s = 10;
System.out.println(s.shortValue());   // Retorna el valor short
System.out.println(s.compareTo((short) 20)); // Compara dos Short
System.out.println(Short.parseShort("100")); // Convierte un String a short
System.out.println(Short.valueOf("50"));  // Convierte un String a Short

// Métodos Comunes a todos los tipos envoltorios
System.out.println(Integer.toString(x)); // Convierte Integer a String
System.out.println(Double.toString(a)); // Convierte Double a String
System.out.println(Boolean.toString(t)); // Convierte Boolean a String
System.out.println(Character.toString(c)); // Convierte Character a String
System.out.println(Long.toString(l)); // Convierte Long a String
System.out.println(Short.toString(s)); // Convierte Short a String

// Autoboxing y Unboxing
Integer num1 = 10;  // Autoboxing (convierte int a Integer)
int n = num1;  // Unboxing (convierte Integer a int)

```
