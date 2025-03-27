```java
// Diferentes maneras de crear un TreeSet
TreeSet<String> set1 = new TreeSet<>(); // Conjunto vacío, ordenado por defecto (orden natural)
TreeSet<String> set2 = new TreeSet<>(Arrays.asList("B", "A", "C")); // Con valores iniciales
TreeSet<Integer> set3 = new TreeSet<>(Comparator.reverseOrder()); // Conjunto con un comparador personalizado (orden descendente)
TreeSet<String> set4 = new TreeSet<>(set2); // Copiar un TreeSet

// Métodos principales de TreeSet
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
set2.first(); // Obtener el primer elemento
set2.last(); // Obtener el último elemento
set2.lower("B"); // Obtener el elemento más bajo que es estrictamente menor a "B"
set2.higher("B"); // Obtener el elemento más alto que es estrictamente mayor a "B"
set2.floor("B"); // Obtener el elemento más cercano y menor o igual a "B"
set2.ceiling("B"); // Obtener el elemento más cercano y mayor o igual a "B"

// Recorridos (mantiene el orden natural o el especificado por el comparador)
for (String elem : set2) {} // For-each
Iterator<String> iterador = set2.iterator(); // Usando Iterator
while (iterador.hasNext()) {
	iterador.next();
}
set2.forEach(e -> {}); // Expresión lambda

// Métodos adicionales
TreeSet<String> copia = new TreeSet<>(set2); // Copiar conjunto
List<String> lista = new ArrayList<>(set2); // Convertir a lista
set2.retainAll(set3); // Conservar solo los elementos en común con otro set
set2.removeAll(set3); // Eliminar los elementos en común con otro set
set2.addAll(set3); // Agregar todos los elementos de otro conjunto

// Método para el ordenamiento personalizado (se usa con un Comparator)
TreeSet<String> set5 = new TreeSet<>(Comparator.comparing(String::length)); // Ordenar por longitud de las cadenas
set5.add("Elemento 1");
set5.add("Elemento 123");
set5.add("Elemento");
```
