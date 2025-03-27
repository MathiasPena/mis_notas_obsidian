```java
// Declaración e inicialización de un Array
int[] array1 = new int[5]; // Array de enteros con 5 elementos (inicializados a 0)
String[] array2 = {"A", "B", "C", "D"}; // Array de cadenas con 4 elementos predefinidos

// Acceso a elementos de un Array
array1[0] = 10; // Asignar valor al primer elemento (índice 0)
String elemento = array2[2]; // Obtener el tercer elemento (índice 2)

// Obtener la longitud de un Array
int longitud = array2.length; // Devuelve el número de elementos en el array

// Recorrido de un Array (usando for-each)
for (String elem : array2) {
	System.out.println(elem); // Recorrer con for-each y mostrar elementos
}

// Recorrido de un Array (usando índice)
for (int i = 0; i < array2.length; i++) {
	System.out.println(array2[i]); // Usar índice para acceder y mostrar elementos
}

// Métodos útiles para manipular Arrays
Arrays.sort(array2); // Ordena los elementos del array (en orden alfabético para Strings)
Arrays.fill(array1, 7); // Rellena todo el array con el valor 7
Arrays.fill(array1, 0, 3, 5); // Rellena una parte del array (índices 0 a 2 con valor 5)

// Copiar un Array
int[] copia = Arrays.copyOf(array1, array1.length); // Copia completa de array1

// Convertir Array a List
List<String> lista = Arrays.asList(array2); // Convierte el array en una List
List<Integer> listaDeEnteros = Arrays.asList(1, 2, 3); // Crear lista con elementos

// Comparación de Arrays (Usando Arrays.equals)
boolean sonIguales = Arrays.equals(array1, copia); // Comparar dos arrays (deben ser del mismo tipo y tener los mismos elementos)

// Buscar un elemento en un Array
int index = Arrays.binarySearch(array2, "C"); // Busca un elemento en un array ordenado (retorna el índice)

// Arrays multidimensionales
int[][] matriz = new int[3][3]; // Array bidimensional (matriz 3x3)
matriz[0][0] = 1; // Asignar valor a una celda de la matriz

// Arrays con diferentes tipos de elementos
Object[] mixedArray = {1, "Texto", 3.14}; // Array de tipo Object que puede almacenar cualquier tipo de objeto
```
