```java
// Anotaciones avanzadas en Java

// @Retention: Define el tiempo de retención de la anotación, es decir, cuándo estará disponible (compilación, ejecución, etc.)
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

@Retention(RetentionPolicy.RUNTIME) // La anotación estará disponible en tiempo de ejecución
public @interface MiAnotacionDeTiempoEjecucion {
    String descripcion() default "Descripción predeterminada";
}

// @Target: Especifica los elementos del programa donde la anotación puede ser utilizada.
import java.lang.annotation.ElementType;
import java.lang.annotation.Target;

@Target(ElementType.METHOD) // La anotación solo puede ser utilizada en métodos
public @interface MiAnotacionDeMetodo {
}

// @Documented: Hace que la anotación sea incluida en la documentación Javadoc
import java.lang.annotation.Documented;

@Documented
@Retention(RetentionPolicy.RUNTIME)
public @interface MiAnotacionDocumentada {
    String descripcion() default "Descripción documentada";
}

// @Inherited: Indica que la anotación será heredada por las subclases
import java.lang.annotation.Inherited;

@Inherited
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE) // Se usa solo en clases
public @interface MiAnotacionHeredada {
    String valor() default "Valor heredado";
}

@MiAnotacionHeredada
class ClaseBase {}

class ClaseHija extends ClaseBase {
    // La ClaseHija hereda la anotación de ClaseBase
}

// @Repeatable: Permite que una anotación sea repetida en el mismo elemento del código
import java.lang.annotation.Repeatable;

@Repeatable(MisAnotaciones.class)
public @interface MiAnotacionRepetible {
    String valor();
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface MisAnotaciones {
    MiAnotacionRepetible[] value(); // Contenedor para las anotaciones repetibles
}

// Ejemplo de uso de @Repeatable
@MiAnotacionRepetible(valor = "Primera anotación")
@MiAnotacionRepetible(valor = "Segunda anotación")
class ClaseConAnotacionesRepetidas {}

// @PostConstruct y @PreDestroy: Se usan para métodos que deben ejecutarse antes o después de que el objeto se cree o destruya (parte del ciclo de vida de un bean en un contexto de inyección de dependencias, como Spring).
import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

class EjemploCicloVida {
    @PostConstruct
    public void inicializar() {
        System.out.println("Objeto inicializado");
    }

    @PreDestroy
    public void destruir() {
        System.out.println("Objeto destruido");
    }
}

// @Entity, @Table, @Column: Anotaciones de JPA (Java Persistence API) que se usan en el contexto de bases de datos para mapear clases a tablas.
import javax.persistence.Entity;
import javax.persistence.Table;
import javax.persistence.Column;

@Entity
@Table(name = "Personas")
public class Persona {
    @Column(name = "nombre")
    private String nombre;

    @Column(name = "edad")
    private int edad;

    // Getters y setters
}

// @Test: Usada en frameworks de pruebas como JUnit para marcar los métodos de prueba.
import org.junit.Test;

public class EjemploTest {
    @Test
    public void pruebaMetodo() {
        // Lógica de prueba
        System.out.println("Método de prueba ejecutado");
    }
}

// @Transaction: Se usa para manejar transacciones en bases de datos (especialmente en contextos como Spring).
import javax.transaction.Transactional;

public class ServicioTransaccion {
    @Transactional
    public void realizarOperacion() {
        // Lógica de operación dentro de una transacción
        System.out.println("Operación dentro de una transacción");
    }
}

```