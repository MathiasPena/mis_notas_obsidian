
```java

import java.util.*; // Importamos todas las utilidades de Java, incluyendo ArrayList

// Diferentes maneras de crear un ArrayList
ArrayList<String> lista1 = new ArrayList<>(); // Lista vacía
ArrayList<String> lista2 = new ArrayList<>(Arrays.asList("A", "B", "C")); // Con elementos iniciales
ArrayList<String> lista3 = new ArrayList<>(10); // Con capacidad inicial definida

// Métodos disponibles en ArrayList:
lista1.add("Elemento 1"); // Agregar un elemento
lista1.add(0, "Elemento 0"); // Insertar en una posición específica
lista1.addAll(lista2); // Agregar todos los elementos de otra lista
lista1.addAll(1, lista2); // Agregar todos los elementos en una posición específica
lista1.set(1, "Nuevo Elemento"); // Modificar un elemento en un índice
lista1.remove(0); // Eliminar por índice
lista1.remove("Elemento 1"); // Eliminar por objeto
lista1.removeAll(lista2); // Eliminar todos los elementos de otra lista
lista1.clear(); // Vaciar la lista

// Métodos de acceso y búsqueda
lista2.get(1); // Obtener elemento en índice específico
lista2.indexOf("B"); // Buscar la primera aparición de un elemento
lista2.lastIndexOf("B"); // Buscar la última aparición de un elemento
lista2.contains("C"); // Verificar si existe el elemento
lista2.isEmpty(); // Verificar si está vacía
lista2.size(); // Obtener cantidad de elementos

// Métodos para convertir y modificar la lista
String[] array = lista2.toArray(new String[0]); // Convertir en array
List<String> subLista = lista2.subList(0, 2); // Obtener una sublista
Collections.sort(lista2); // Ordenar la lista
Collections.reverse(lista2); // Invertir la lista
Collections.shuffle(lista2); // Mezclar aleatoriamente

// Recorridos
for (String elem : lista2) {} // For-each
for (int i = 0; i < lista2.size(); i++) {} // For clásico
Iterator<String> iterador = lista2.iterator(); // Usando Iterator
while (iterador.hasNext()) {
	iterador.next();
}
lista2.forEach(e -> {}); // Expresión lambda

// Métodos adicionales
lista2.ensureCapacity(20); // Asegurar capacidad mínima
lista2.trimToSize(); // Ajustar tamaño al número de elementos
List<String> copia = new ArrayList<>(lista2); // Copiar lista
```
