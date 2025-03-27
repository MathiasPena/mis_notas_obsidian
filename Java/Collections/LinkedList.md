
```java

import java.util.*; // Importamos todas las utilidades de Java, incluyendo LinkedList

// Diferentes maneras de crear una LinkedList
LinkedList<String> lista1 = new LinkedList<>(); // Lista vacía
LinkedList<String> lista2 = new LinkedList<>(Arrays.asList("A", "B", "C")); // Con elementos iniciales

// Métodos disponibles en LinkedList:
lista1.add("Elemento 1"); // Agregar un elemento al final
lista1.add(0, "Elemento 0"); // Insertar en una posición específica
lista1.addAll(lista2); // Agregar todos los elementos de otra lista
lista1.addFirst("Inicio"); // Agregar al inicio
lista1.addLast("Fin"); // Agregar al final
lista1.set(1, "Nuevo Elemento"); // Modificar un elemento en un índice
lista1.remove(0); // Eliminar por índice
lista1.remove("Elemento 1"); // Eliminar por objeto
lista1.removeFirst(); // Eliminar el primer elemento
lista1.removeLast(); // Eliminar el último elemento
lista1.clear(); // Vaciar la lista

// Métodos de acceso y búsqueda
lista2.get(1); // Obtener elemento en índice específico
lista2.getFirst(); // Obtener el primer elemento
lista2.getLast(); // Obtener el último elemento
lista2.indexOf("B"); // Buscar la primera aparición de un elemento
lista2.lastIndexOf("B"); // Buscar la última aparición de un elemento
lista2.contains("C"); // Verificar si existe el elemento
lista2.isEmpty(); // Verificar si está vacía
lista2.size(); // Obtener cantidad de elementos

// Métodos para manipular la estructura
lista2.poll(); // Obtener y eliminar el primer elemento (o null si vacío)
lista2.pollFirst(); // Igual que poll(), pero explícito
lista2.pollLast(); // Obtener y eliminar el último elemento
lista2.peek(); // Obtener el primer elemento sin eliminarlo
lista2.peekFirst(); // Igual que peek(), pero explícito
lista2.peekLast(); // Obtener el último elemento sin eliminarlo
lista2.push("X"); // Insertar al inicio (como en pila)
lista2.pop(); // Extraer el primer elemento (como en pila)

// Recorridos
for (String elem : lista2) {} // For-each
for (int i = 0; i < lista2.size(); i++) {} // For clásico
Iterator<String> iterador = lista2.iterator(); // Usando Iterator
while (iterador.hasNext()) {
	iterador.next();
}
lista2.forEach(e -> {}); // Expresión lambda

// Métodos adicionales
List<String> copia = new LinkedList<>(lista2); // Copiar lista
Collections.sort(lista2); // Ordenar la lista
Collections.reverse(lista2); // Invertir la lista
Collections.shuffle(lista2); // Mezclar aleatoriamente
 ```