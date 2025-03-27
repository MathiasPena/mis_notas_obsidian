```java
// Diferentes maneras de crear un LinkedHashSet
LinkedHashSet<String> set1 = new LinkedHashSet<>(); // Conjunto vacío
LinkedHashSet<String> set2 = new LinkedHashSet<>(Arrays.asList("A", "B", "C")); // Con valores iniciales
LinkedHashSet<String> set3 = new LinkedHashSet<>(10); // Con capacidad inicial definida
LinkedHashSet<String> set4 = new LinkedHashSet<>(10, 0.75f); // Con capacidad y factor de carga

// Agregar elementos
set1.add("Elemento 1");
set1.add("Elemento 2"); 
set1.add("Elemento 1"); // No se permiten duplicados, no se añadirá otra vez
set1.addAll(set2); // Agregar todos los elementos de otro conjunto

// Eliminar elementos
set1.remove("Elemento 2"); // Eliminar por valor
set1.clear(); // Vaciar el conjunto

// Métodos de verificación y consulta
boolean contiene = set2.contains("A"); // Verificar si contiene un elemento
boolean estaVacio = set2.isEmpty(); // Verificar si está vacío
int tamanio = set2.size(); // Obtener el número de elementos

// Recorridos (mantiene el orden de inserción)
for (String elem : set2) {
	// Iterar con for-each
}
Iterator<String> iterador = set2.iterator(); // Usando Iterator
while (iterador.hasNext()) {
	String elemento = iterador.next();
}
set2.forEach(e -> { 
	// Expresión lambda
});

// Métodos adicionales
LinkedHashSet<String> copia = new LinkedHashSet<>(set2); // Copiar conjunto
List<String> lista = new ArrayList<>(set2); // Convertir a lista
set2.retainAll(set3); // Conservar solo los elementos en común con otro set
set2.removeAll(set3); // Eliminar los elementos en común con otro set
Object[] array = set2.toArray(); // Convertir a array
String[] arrayStrings = set2.toArray(new String[0]); // Convertir a array de Strings

// Comprobación de igualdad
boolean esIgual = set2.equals(set3); // Comparar con otro conjunto
int hashCode = set2.hashCode(); // Obtener código hash del conjunto
```
