```java
// Crear una lista de objetos
List<String> lista = Arrays.asList("Banana", "Apple", "Mango", "Pineapple");

// Ordenar utilizando un Comparator con lambda
Collections.sort(lista, (s1, s2) -> s1.compareTo(s2)); // Orden alfabético ascendente

// Ordenar en orden inverso con un Comparator con lambda
Collections.sort(lista, (s1, s2) -> s2.compareTo(s1)); // Orden alfabético descendente

// Crear un Comparator usando una clase que implemente Comparator
Comparator<String> comparator = new StringLengthComparator();
Collections.sort(lista, comparator); // Ordenar por longitud de las cadenas

// Ordenar usando un Comparator con method reference
Collections.sort(lista, Comparator.naturalOrder()); // Orden ascendente (igual a compareTo)
Collections.sort(lista, Comparator.reverseOrder()); // Orden descendente

// Ordenar usando thenComparing (comparator encadenado)
List<Person> personas = Arrays.asList(
	new Person("John", 25),
	new Person("Jane", 22),
	new Person("Alice", 25)
);
personas.sort(Comparator.comparing(Person::getAge).thenComparing(Person::getName)); // Orden primero por edad, luego por nombre

// Comparador inverso
Collections.sort(lista, Comparator.reverseOrder()); // Inversión del orden natural
}

// Comparador de longitud de cadenas
static class StringLengthComparator implements Comparator<String> {
@Override
public int compare(String s1, String s2) {
	return Integer.compare(s1.length(), s2.length()); // Ordenar por longitud de la cadena
}
}

// Clase Person para ilustrar el uso de comparators con objetos
static class Person {
String name;
int age;

Person(String name, int age) {
	this.name = name;
	this.age = age;
}

public String getName() {
	return name;
}

public int getAge() {
	return age;
}
```