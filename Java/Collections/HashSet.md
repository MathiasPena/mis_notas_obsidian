```java
// Diferentes maneras de crear un HashSet
HashSet<String> set1 = new HashSet<>(); // Conjunto vacío
HashSet<String> set2 = new HashSet<>(Arrays.asList("A", "B", "C")); // Con valores iniciales
HashSet<String> set3 = new HashSet<>(10); // Con capacidad inicial definida
HashSet<String> set4 = new HashSet<>(10, 0.75f); // Con capacidad y factor de carga

// Métodos principales de HashSet
set1.add("Elemento 1"); // Agregar un elemento
set1.add("Elemento 2"); 
set1.add("Elemento 1"); // No se permiten duplicados, no se añadirá otra vez
set1.addAll(set2); // Agregar todos los elementos de otro conjunto
set1.remove("Elemento 2"); // Eliminar un elemento
set1.clear(); // Vaciar el conjunto

// Métodos de verificación y consulta
set2.contains("A"); // Verificar si contiene un elemento
set2.isEmpty(); // Verificar si está vacío
set2.size(); // Obtener el número de elementos

// Recorridos
for (String elem : set2) {} // For-each
Iterator<String> iterador = set2.iterator(); // Usando Iterator
while (iterador.hasNext()) {
	iterador.next();
}
set2.forEach(e -> {}); // Expresión lambda

// Métodos adicionales
HashSet<String> copia = new HashSet<>(set2); // Copiar conjunto
List<String> lista = new ArrayList<>(set2); // Convertir a lista
set2.retainAll(set3); // Conservar solo los elementos en común con otro set
set2.removeAll(set3); // Eliminar los elementos en común con otro set
```
