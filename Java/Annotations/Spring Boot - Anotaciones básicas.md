```java
// Anotaciones básicas de Spring Boot

// @SpringBootApplication: Anotación principal que habilita la configuración automática, escaneo de componentes y configuración de Spring
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.SpringApplication;

@SpringBootApplication // Se usa en la clase principal para arrancar la aplicación Spring Boot
public class MiAplicacion {
    public static void main(String[] args) {
        SpringApplication.run(MiAplicacion.class, args); // Arranca la aplicación
    }
}

// @RestController: Indica que una clase es un controlador REST (comúnmente usado en APIs RESTful)
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.GetMapping;

@RestController // Marca la clase como un controlador REST
public class MiControlador {
    
    @GetMapping("/saludo") // Mapea la ruta /saludo a este método
    public String saludo() {
        return "Hola Mundo";
    }
}

// @RequestMapping: Define un mapeo genérico para solicitudes HTTP (GET, POST, etc.)
import org.springframework.web.bind.annotation.RequestMapping;

@RequestMapping("/api") // Mapea la ruta base para todos los métodos de la clase
public class ControladorGeneral {

    @RequestMapping("/consulta")
    public String obtenerDatos() {
        return "Datos consultados";
    }
}

// @GetMapping, @PostMapping, @PutMapping, @DeleteMapping: Métodos especializados para manejar tipos específicos de solicitudes HTTP
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;

public class MiControlador {
    
    @GetMapping("/obtener")
    public String obtener() {
        return "Obtención de datos";
    }

    @PostMapping("/crear")
    public String crear(@RequestBody String datos) {
        return "Creación de datos: " + datos;
    }
}

// @Component: Marca una clase como un componente gestionado por Spring, lo que permite la inyección de dependencias
import org.springframework.stereotype.Component;

@Component // Hace que esta clase sea un componente gestionado por Spring
public class MiComponente {
    public void saludar() {
        System.out.println("Hola desde el componente");
    }
}

// @Service: Indica que la clase es un servicio en la capa de negocio
import org.springframework.stereotype.Service;

@Service // Marca la clase como un servicio
public class MiServicio {
    public void realizarOperacion() {
        System.out.println("Operación realizada");
    }
}

// @Repository: Marca una clase como un componente de acceso a datos (DAO) para la capa de persistencia
import org.springframework.stereotype.Repository;

@Repository // Marca la clase como un repositorio (gestiona datos)
public class MiRepositorio {
    public void guardar() {
        System.out.println("Datos guardados");
    }
}

// @Autowired: Inyección de dependencias, permite inyectar automáticamente un bean en otro
import org.springframework.beans.factory.annotation.Autowired;

public class MiControlador {

    @Autowired // Inyección automática del servicio
    private MiServicio miServicio;

    public void ejecutarServicio() {
        miServicio.realizarOperacion();
    }
}

// @Value: Inyección de valores de propiedades o configuraciones
import org.springframework.beans.factory.annotation.Value;

public class MiConfiguracion {

    @Value("${app.name}") // Inyecta el valor de la propiedad 'app.name' en el archivo application.properties
    private String appName;

    public void mostrarNombreApp() {
        System.out.println("Nombre de la aplicación: " + appName);
    }
}

// @Configuration: Indica que la clase contiene configuraciones de beans de Spring
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration // Marca la clase como una clase de configuración
public class MiConfiguracion {

    @Bean // Define un bean que será gestionado por Spring
    public MiComponente miComponente() {
        return new MiComponente();
    }
}

// @EnableAutoConfiguration: Habilita la configuración automática en Spring Boot (usado internamente por @SpringBootApplication)
import org.springframework.context.annotation.EnableAutoConfiguration;

@EnableAutoConfiguration // Habilita la configuración automática
public class MiAplicacion {
    public static void main(String[] args) {
        SpringApplication.run(MiAplicacion.class, args);
    }
}

```
