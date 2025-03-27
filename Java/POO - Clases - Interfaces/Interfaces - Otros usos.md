```java
// Uso de Interfaces en Java

// 1. Polimorfismo
interface Forma {
    void dibujar();
}

class Circulo implements Forma {
    @Override
    public void dibujar() {
        System.out.println("Dibujando un círculo");
    }
}

class Cuadrado implements Forma {
    @Override
    public void dibujar() {
        System.out.println("Dibujando un cuadrado");
    }
}

public class Main {
    public static void main(String[] args) {
        Forma forma1 = new Circulo();
        Forma forma2 = new Cuadrado();

        forma1.dibujar(); // Output: Dibujando un círculo
        forma2.dibujar(); // Output: Dibujando un cuadrado
    }
}

// 2. Desacoplamiento y Flexibilidad
interface BaseDeDatos {
    void conectar();
    void desconectar();
}

class MySQL implements BaseDeDatos {
    @Override
    public void conectar() {
        System.out.println("Conectando a MySQL");
    }

    @Override
    public void desconectar() {
        System.out.println("Desconectando de MySQL");
    }
}

class PostgreSQL implements BaseDeDatos {
    @Override
    public void conectar() {
        System.out.println("Conectando a PostgreSQL");
    }

    @Override
    public void desconectar() {
        System.out.println("Desconectando de PostgreSQL");
    }
}

public class Main {
    public static void main(String[] args) {
        BaseDeDatos db = new MySQL();
        db.conectar();  // Output: Conectando a MySQL
        db.desconectar();  // Output: Desconectando de MySQL
        
        db = new PostgreSQL();
        db.conectar();  // Output: Conectando a PostgreSQL
        db.desconectar();  // Output: Desconectando de PostgreSQL
    }
}

// 3. Implementación de Múltiples Interfaces
interface Volador {
    void volar();
}

interface Nadador {
    void nadar();
}

class Pato implements Volador, Nadador {
    @Override
    public void volar() {
        System.out.println("El pato vuela");
    }

    @Override
    public void nadar() {
        System.out.println("El pato nada");
    }
}

public class Main {
    public static void main(String[] args) {
        Pato pato = new Pato();
        pato.volar();  // Output: El pato vuela
        pato.nadar();  // Output: El pato nada
    }
}

// 4. Facilitar la Comunicación entre Componentes en un Sistema
interface Almacenamiento {
    void guardar(String archivo);
    String cargar(String archivo);
}

class DiscoDuro implements Almacenamiento {
    @Override
    public void guardar(String archivo) {
        System.out.println("Guardando " + archivo + " en el disco duro");
    }

    @Override
    public String cargar(String archivo) {
        return "Cargando " + archivo + " desde el disco duro";
    }
}

public class Main {
    public static void main(String[] args) {
        Almacenamiento almacenamiento = new DiscoDuro();
        almacenamiento.guardar("documento.txt");
        System.out.println(almacenamiento.cargar("documento.txt"));
    }
}

// 5. Trabajo con Colecciones y Funcionalidad Adicional
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> lista = new ArrayList<>();
        lista.add("Java");
        lista.add("Python");
        lista.add("C++");

        // Se puede cambiar fácilmente el tipo de la lista
        // Lista de LinkedList, pero sigue implementando la interfaz List
        List<String> otraLista = new LinkedList<>(lista);

        for (String lenguaje : otraLista) {
            System.out.println(lenguaje);
        }
    }
}

// 6. Mejorar la Legibilidad y Mantenimiento del Código
interface Almacenamiento {
    void guardar(String archivo);
    String cargar(String archivo);
}

class DiscoDuro implements Almacenamiento {
    @Override
    public void guardar(String archivo) {
        System.out.println("Guardando " + archivo + " en el disco duro");
    }

    @Override
    public String cargar(String archivo) {
        return "Cargando " + archivo + " desde el disco duro";
    }
}

public class Main {
    public static void main(String[] args) {
        Almacenamiento almacenamiento = new DiscoDuro();
        almacenamiento.guardar("documento.txt");
        System.out.println(almacenamiento.cargar("documento.txt"));
    }
}

```
