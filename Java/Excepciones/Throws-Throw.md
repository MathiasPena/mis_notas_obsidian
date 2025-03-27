```java
try {
	metodoConThrows(); // Este método puede lanzar una excepción
} catch (ArithmeticException e) {
	System.out.println("Capturada excepción: " + e.getMessage());
}

try {
	validarEdad(15); // Provocará una excepción personalizada
} catch (IllegalArgumentException e) {
	System.out.println("Error: " + e.getMessage());
}


// Uso de throws para indicar que el método puede lanzar una excepción
public static void metodoConThrows() throws ArithmeticException {
int resultado = 10 / 0; // Provoca ArithmeticException
}

// Uso de throw para lanzar una excepción manualmente
public static void validarEdad(int edad) {
if (edad < 18) {
	throw new IllegalArgumentException("La edad debe ser mayor o igual a 18.");
}
System.out.println("Edad válida: " + edad);
}
```
