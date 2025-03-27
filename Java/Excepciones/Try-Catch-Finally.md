```java
// Uso básico de try-catch-finally
try {
	int resultado = 10 / 0; // Provoca una excepción (división por cero)
} catch (ArithmeticException e) {
	System.out.println("Error: División por cero.");
} finally {
	System.out.println("Este bloque se ejecuta siempre.");
}

// Múltiples bloques catch
try {
	String texto = null;
	System.out.println(texto.length()); // Provoca NullPointerException
} catch (NullPointerException e) {
	System.out.println("Error: Intento de acceder a un objeto nulo.");
} catch (Exception e) {
	System.out.println("Error general: " + e.getMessage());
} finally {
	System.out.println("Este finally también se ejecuta.");
}

// try-catch anidado
try {
	try {
		int[] numeros = {1, 2, 3};
		System.out.println(numeros[5]); // Provoca ArrayIndexOutOfBoundsException
	} catch (ArrayIndexOutOfBoundsException e) {
		System.out.println("Error: Índice fuera de rango.");
		throw e; // Relanzamos la excepción
	}
} catch (Exception e) {
	System.out.println("Capturada en el catch externo: " + e);
}

// Uso de try con recursos (try-with-resources)
try (java.io.FileReader fr = new java.io.FileReader("archivo.txt")) {
	System.out.println("Archivo leído correctamente.");
} catch (java.io.IOException e) {
	System.out.println("Error al leer el archivo.");
} finally {
	System.out.println("Fin del manejo de archivo.");
}
```
