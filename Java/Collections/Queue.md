```java
// Diferentes maneras de crear una Queue
Queue<String> queue1 = new LinkedList<>(); // Usamos LinkedList para crear una Queue
Queue<String> queue2 = new PriorityQueue<>(); // Usamos PriorityQueue para crear una Queue
Queue<String> queue3 = new ArrayDeque<>(); // Usamos ArrayDeque para crear una Queue

// Métodos principales de Queue
queue1.offer("Elemento 1"); // Agregar un elemento a la Queue
queue1.offer("Elemento 2");
queue1.offer("Elemento 3");
queue1.offer("Elemento 4");

String first = queue1.peek(); // Ver el primer elemento (sin eliminarlo)
String removed = queue1.poll(); // Eliminar y devolver el primer elemento
boolean isEmpty = queue1.isEmpty(); // Verificar si la Queue está vacía
int size = queue1.size(); // Obtener el tamaño de la Queue

// Métodos de consulta
boolean contains = queue2.contains("Elemento 1"); // Verificar si un elemento está en la Queue
String firstElement = queue1.peek(); // Obtener el primer elemento (sin eliminarlo)

// Recorridos
for (String elem : queue2) { // Recorrer con for-each
	System.out.println(elem);
}

Iterator<String> iterator = queue1.iterator(); // Usar un Iterator para recorrer
while (iterator.hasNext()) {
	String elem = iterator.next();
	System.out.println(elem);
}

// Ejemplo de uso de Queue como cola de procesamiento
Queue<String> procesamiento = new LinkedList<>();
procesamiento.offer("Tarea 1");
procesamiento.offer("Tarea 2");
procesamiento.offer("Tarea 3");

// Procesar tareas en orden FIFO
while (!procesamiento.isEmpty()) {
	String tarea = procesamiento.poll();
	System.out.println("Procesando: " + tarea);
}

// Métodos adicionales
Queue<String> copia = new LinkedList<>(queue1); // Copiar el contenido de una Queue a otra
Queue<String> otraQueue = new LinkedList<>();
otraQueue.offer("Elemento A");
otraQueue.offer("Elemento B");
queue1.addAll(otraQueue); // Agregar todos los elementos de otra Queue

// Usos de otras implementaciones de Queue

// PriorityQueue: Mantiene los elementos en orden natural o por un comparador proporcionado
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(5);
pq.offer(1);
pq.offer(3);

// Los elementos salen en orden natural (de menor a mayor)
while (!pq.isEmpty()) {
	System.out.println("Procesando: " + pq.poll());
}

// ArrayDeque: No tiene la sobrecarga de los métodos de LinkedList
ArrayDeque<String> deque = new ArrayDeque<>();
deque.offerFirst("Elemento 1"); // Agregar al principio
deque.offerLast("Elemento 2"); // Agregar al final
deque.pollFirst(); // Eliminar el primer elemento
deque.pollLast(); // Eliminar el último elemento
```