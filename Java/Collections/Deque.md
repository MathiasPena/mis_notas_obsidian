```java
// Diferentes maneras de crear un Deque
Deque<String> deque1 = new LinkedList<>(); // Usamos LinkedList para crear un Deque
Deque<String> deque2 = new ArrayDeque<>(); // Usamos ArrayDeque para crear un Deque

// Métodos principales de Deque
deque1.offerFirst("Elemento 1"); // Agregar un elemento al principio
deque1.offerLast("Elemento 2"); // Agregar un elemento al final
deque1.addFirst("Elemento 3"); // Agregar un elemento al principio (diferente de offerFirst)
deque1.addLast("Elemento 4"); // Agregar un elemento al final (diferente de offerLast)

String first = deque1.peekFirst(); // Obtener el primer elemento sin eliminarlo
String last = deque1.peekLast(); // Obtener el último elemento sin eliminarlo

String removedFirst = deque1.pollFirst(); // Eliminar el primer elemento y devolverlo
String removedLast = deque1.pollLast(); // Eliminar el último elemento y devolverlo

boolean isEmpty = deque1.isEmpty(); // Verificar si el Deque está vacío
int size = deque1.size(); // Obtener el tamaño del Deque

// Métodos adicionales de consulta
boolean contains = deque2.contains("Elemento 1"); // Verificar si un elemento está en el Deque
String firstElem = deque1.peekFirst(); // Ver el primer elemento sin eliminarlo
String lastElem = deque1.peekLast(); // Ver el último elemento sin eliminarlo

// Recorridos (usando for-each y iterador)
for (String elem : deque1) { // Recorrer con for-each
	System.out.println(elem);
}

Iterator<String> iterator = deque1.iterator(); // Usar un Iterator para recorrer
while (iterator.hasNext()) {
	String elem = iterator.next();
	System.out.println(elem);
}

// Ejemplo de uso de Deque como una cola de tareas (FIFO) y pila (LIFO)
Deque<String> tareas = new LinkedList<>();
tareas.offerFirst("Tarea 1"); // Agregar al principio
tareas.offerLast("Tarea 2");  // Agregar al final
tareas.addFirst("Tarea 3");  // Agregar al principio
tareas.addLast("Tarea 4");   // Agregar al final

// Procesar tareas en orden FIFO (primero en entrar, primero en salir)
while (!tareas.isEmpty()) {
	String tarea = tareas.pollFirst(); // Sacar del principio
	System.out.println("Procesando: " + tarea);
}

// Pila de tareas (LIFO) - Agregar al final y sacar desde el principio
Deque<String> pilaTareas = new LinkedList<>();
pilaTareas.push("Tarea A"); // Agregar al final (como en una pila)
pilaTareas.push("Tarea B"); // Agregar al final
pilaTareas.push("Tarea C"); // Agregar al final

// Procesar tareas en orden LIFO (último en entrar, primero en salir)
while (!pilaTareas.isEmpty()) {
	String tarea = pilaTareas.pop(); // Sacar desde el final
	System.out.println("Procesando: " + tarea);
}

// Métodos adicionales
Deque<String> copiaDeque = new LinkedList<>(deque1); // Copiar el contenido de un Deque a otro
Deque<String> otraDeque = new LinkedList<>();
otraDeque.offer("Elemento A");
otraDeque.offer("Elemento B");
deque1.addAll(otraDeque); // Agregar todos los elementos de otro Deque

// Otros métodos que puedes usar
deque1.removeFirst(); // Eliminar el primer elemento
deque1.removeLast();  // Eliminar el último elemento
deque1.getFirst();    // Obtener el primer elemento
deque1.getLast();     // Obtener el último elemento
```
