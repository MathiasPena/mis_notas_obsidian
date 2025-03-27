```java
// Diferentes maneras de crear un LinkedHashMap
LinkedHashMap<String, Integer> map1 = new LinkedHashMap<>(); // Mapa vacío
LinkedHashMap<String, Integer> map2 = new LinkedHashMap<>(10); // Mapa con capacidad inicial
LinkedHashMap<String, Integer> map3 = new LinkedHashMap<>(10, 0.75f); // Mapa con capacidad inicial y factor de carga
LinkedHashMap<String, Integer> map4 = new LinkedHashMap<>(map1); // Copiar otro LinkedHashMap
LinkedHashMap<String, Integer> map5 = new LinkedHashMap<>(10, 0.75f, true); // Mapa con acceso ordenado por acceso (no por inserción)

// Métodos principales de LinkedHashMap
map1.put("A", 1); // Agregar un par clave-valor
map1.put("B", 2);
map1.put("C", 3);
map1.put("A", 4); // Si ya existe la clave, se reemplaza el valor
map1.putAll(map2); // Agregar todos los elementos de otro mapa
map1.remove("B"); // Eliminar un par clave-valor por la clave
map1.clear(); // Vaciar el mapa

// Métodos de verificación y consulta
map2.containsKey("A"); // Verificar si existe una clave
map2.containsValue(3); // Verificar si existe un valor
map2.isEmpty(); // Verificar si está vacío
map2.size(); // Obtener el número de pares clave-valor
map2.get("A"); // Obtener el valor asociado a una clave
map2.getOrDefault("D", 0); // Obtener valor por clave, o valor por defecto si no existe

// Recorridos (mantiene el orden de inserción o acceso)
for (Map.Entry<String, Integer> entry : map2.entrySet()) { // Recorrer claves y valores
	String key = entry.getKey();
	Integer value = entry.getValue();
}

map2.forEach((key, value) -> { // Expresión lambda para recorrer claves y valores
	System.out.println(key + ": " + value);
});

// Métodos adicionales
LinkedHashMap<String, Integer> copia = new LinkedHashMap<>(map2); // Copiar mapa
Set<String> claves = map2.keySet(); // Obtener solo las claves
Collection<Integer> valores = map2.values(); // Obtener solo los valores
List<Map.Entry<String, Integer>> lista = new ArrayList<>(map2.entrySet()); // Convertir a lista

// Métodos de comparación y orden
map2.entrySet().stream() // Ordenar por valor de manera ascendente
	.sorted(Map.Entry.comparingByValue())
	.forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));

map2.entrySet().stream() // Ordenar por valor de manera descendente
	.sorted(Map.Entry.comparingByValue(Comparator.reverseOrder()))
	.forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));

// Métodos para reemplazar valores
map2.replace("A", 10); // Reemplazar valor por clave
map2.replace("B", 2, 20); // Reemplazar solo si el valor actual es 2
map2.replaceAll((key, value) -> value * 2); // Reemplazar todos los valores con una función

// Métodos de comparación
map2.equals(map3); // Comparar si dos mapas son iguales
map2.hashCode(); // Obtener el código hash del mapa

// Métodos adicionales para rendimiento
map2.computeIfAbsent("D", key -> 5); // Si no existe la clave "D", agregarla con valor 5
map2.computeIfPresent("A", (key, value) -> value + 1); // Si la clave existe, modificar su valor

// Método para combinar el valor actual con una nueva operación
map2.merge("A", 10, (oldValue, newValue) -> oldValue + newValue); // Sumar el valor existente con el nuevo valor

// Acceso ordenado por acceso
LinkedHashMap<String, Integer> map6 = new LinkedHashMap<>(10, 0.75f, true); // El orden de acceso es el que marca el último acceso
map6.put("X", 1);
map6.put("Y", 2);
map6.put("Z", 3);

map6.get("Y"); // Acceder a "Y", esto lo mueve al final del mapa

// Recorridos en orden de acceso
for (Map.Entry<String, Integer> entry : map6.entrySet()) { // Se imprimirá X, Z, Y debido al orden de acceso
	String key = entry.getKey();
	Integer value = entry.getValue();
```