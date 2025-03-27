```java
// Diferentes maneras de crear un List
List<String> lista1 = new ArrayList<>(); // Usamos ArrayList, es eficiente para acceder por índice
List<String> lista2 = new LinkedList<>(); // Usamos LinkedList, es eficiente para insertar y eliminar

// Métodos principales de List
lista1.add("Elemento 1"); // Agregar un elemento al final de la lista
lista1.add("Elemento 2"); // Agregar otro elemento
lista1.add(1, "Elemento 3"); // Insertar un elemento en una posición específica (índice 1)

lista1.set(0, "Elemento Modificado"); // Modificar un elemento en una posición específica (índice 0)

String elem = lista1.get(1); // Obtener el elemento en la posición 1 (índice)
String removed = lista1.remove(1); // Eliminar el elemento en la posición 1 y devolverlo

boolean contains = lista1.contains("Elemento 2"); // Verificar si un elemento está en la lista
int index = lista1.indexOf("Elemento 2"); // Obtener el índice del primer elemento encontrado
int lastIndex = lista1.lastIndexOf("Elemento 2"); // Obtener el índice del último elemento encontrado

List<String> sublista = lista1.subList(0, 2); // Obtener una sublista de elementos desde el índice 0 hasta el 2 (sin incluir el índice 2)

boolean isEmpty = lista1.isEmpty(); // Verificar si la lista está vacía
int size = lista1.size(); // Obtener el tamaño de la lista

// Recorridos (usando for-each y un Iterator)
for (String elem : lista1) { // Recorrer con for-each
	System.out.println(elem);
}

Iterator<String> iterator = lista1.iterator(); // Usar un Iterator para recorrer
while (iterator.hasNext()) {
	String elem = iterator.next();
	System.out.println(elem);
}

// Conversión entre List y otras colecciones
Set<String> set = new HashSet<>(lista1); // Convertir un List a un Set (eliminando duplicados)
List<String> listaCopia = new ArrayList<>(lista1); // Hacer una copia de la lista

// Métodos adicionales
lista1.addAll(lista2); // Agregar todos los elementos de otra lista a la lista actual
lista1.removeAll(lista2); // Eliminar todos los elementos de lista2 de lista1
lista1.retainAll(lista2); // Mantener solo los elementos comunes entre lista1 y lista2

// Métodos para obtener elementos en diferentes posiciones
String firstElem = lista1.get(0); // Obtener el primer elemento (índice 0)
String lastElem = lista1.get(lista1.size() - 1); // Obtener el último elemento

// Limpiar la lista
lista1.clear(); // Eliminar todos los elementos de la lista
```
