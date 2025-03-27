```java
// Diferentes maneras de crear un Stack
Stack<String> stack1 = new Stack<>(); // Crear un stack vacío
Stack<String> stack2 = new Stack<>();
stack2.push("A"); // Agregar un elemento al stack
stack2.push("B");
stack2.push("C");

// Métodos principales de Stack
stack1.push("Elemento 1"); // Agregar un elemento
stack1.push("Elemento 2");
stack1.push("Elemento 3");
stack1.push("Elemento 4");

String top = stack1.peek(); // Ver el elemento en la cima (sin quitarlo)
String popElem = stack1.pop(); // Eliminar y devolver el elemento en la cima
boolean isEmpty = stack1.isEmpty(); // Verificar si el stack está vacío
int size = stack1.size(); // Obtener el tamaño del stack

// Métodos de consulta
stack2.contains("B"); // Verificar si el stack contiene un elemento
stack2.search("A"); // Buscar la posición de un elemento, devuelve la distancia desde la cima

// Recorridos
for (String elem : stack2) { // Recorrer con for-each
	System.out.println(elem);
}

Iterator<String> iterador = stack2.iterator(); // Usando Iterator
while (iterador.hasNext()) {
	String elem = iterador.next();
	System.out.println(elem);
}

// Métodos adicionales
Stack<String> copia = (Stack<String>) stack2.clone(); // Clonar el stack
Stack<String> stack3 = new Stack<>(); // Otro stack para demostración de métodos
stack3.addAll(stack2); // Agregar todos los elementos de otro stack

// Vaciado del stack
stack1.clear(); // Vaciar el stack
System.out.println("Stack vacío: " + stack1.isEmpty());

// Método de búsqueda
int position = stack2.search("B"); // Devuelve la posición de un elemento (contando desde 1)
System.out.println("Posición de B: " + position); // Si no lo encuentra, devuelve -1

// Métodos de seguridad
try {
	String popped = stack2.pop(); // Elimina y devuelve el último elemento
	System.out.println("Elemento eliminado: " + popped);
} catch (EmptyStackException e) {
	System.out.println("No se puede hacer pop, el stack está vacío.");
}

// Ejemplo de uso en una expresión matemática (evaluación de paréntesis)
String expresion = "( ( 1 + 2 ) * ( 3 + 4 ) )";
Stack<Character> parenStack = new Stack<>();
for (int i = 0; i < expresion.length(); i++) {
	char c = expresion.charAt(i);
	if (c == '(') {
		parenStack.push(c); // Push cuando encontramos un '('
	} else if (c == ')') {
		if (!parenStack.isEmpty()) {
			parenStack.pop(); // Pop cuando encontramos un ')'
		} else {
			System.out.println("Paréntesis no balanceados");
		}
	}
}
if (parenStack.isEmpty()) {
	System.out.println("Paréntesis balanceados.");
} else {
	System.out.println("Paréntesis no balanceados.");
}
```
