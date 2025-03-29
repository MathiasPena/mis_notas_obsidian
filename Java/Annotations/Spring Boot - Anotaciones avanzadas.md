```java
// Anotaciones avanzadas de Spring Boot

// @Bean: Define un bean dentro de una clase de configuración. Este bean será gestionado por el contexto de Spring.
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class ConfiguracionAvanzada {
    
    @Bean // Crea un bean de tipo MiComponente
    public MiComponente miComponente() {
        return new MiComponente();
    }
}

// @EnableAspectJAutoProxy: Activa el soporte para AOP (Programación Orientada a Aspectos) en Spring.
import org.springframework.context.annotation.EnableAspectJAutoProxy;

@EnableAspectJAutoProxy // Activa el proxy de aspectos
public class ConfiguracionAOP {
    // Aquí se pueden definir aspectos para interceptar métodos y aplicar lógica adicional
}

// @EnableScheduling: Habilita el soporte para tareas programadas en Spring (usado para configurar tareas cron).
import org.springframework.scheduling.annotation.EnableScheduling;

@EnableScheduling // Activa la ejecución de tareas programadas (como con cron)
public class ConfiguracionTareas {
    // Aquí se pueden definir métodos para ejecutar en intervalos específicos
}

// @Scheduled: Define un método que debe ejecutarse según un cron o intervalo de tiempo.
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
public class MiTareaProgramada {

    @Scheduled(fixedRate = 5000) // Ejecuta cada 5 segundos
    public void tarea() {
        System.out.println("Ejecutando tarea programada...");
    }
    
    @Scheduled(cron = "0 0 12 * * ?") // Ejecuta a las 12 del mediodía todos los días
    public void tareaCron() {
        System.out.println("Ejecutando tarea cron...");
    }
}

// @Profile: Define un bean que solo se activa si el perfil de Spring coincide con el perfil indicado.
import org.springframework.context.annotation.Profile;
import org.springframework.stereotype.Component;

@Component
@Profile("dev") // Este bean solo se crea si el perfil de Spring es 'dev'
public class MiComponenteDev {
    // Bean específico para el entorno de desarrollo
}

// @PropertySource: Especifica un archivo de propiedades externo que será cargado en el contexto de Spring.
import org.springframework.context.annotation.PropertySource;

@PropertySource("classpath:config.properties") // Carga propiedades desde 'config.properties'
public class ConfiguracionPropiedades {
    // Las propiedades se pueden inyectar en los beans usando @Value
}

// @RestControllerAdvice: Combinación de @ControllerAdvice y @RestController. Permite manejar excepciones globalmente en controladores REST.
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

@RestControllerAdvice
public class ExcepcionGlobal {

    @ExceptionHandler(Exception.class)
    public String manejarExcepcion(Exception ex) {
        return "Ocurrió un error: " + ex.getMessage();
    }
}

// @RequestScope: Marca un bean como de alcance de solicitud, se crea por cada solicitud HTTP.
import org.springframework.context.annotation.Scope;
import org.springframework.web.context.annotation.RequestScope;

@RequestScope // El bean se crea para cada solicitud HTTP
public class MiBeanDeSolicitud {
    // Este bean es creado cada vez que una solicitud es recibida
}

// @SessionScope: Marca un bean como de alcance de sesión, se crea una vez por sesión de usuario.
import org.springframework.web.context.annotation.SessionScope;

@SessionScope // El bean se crea una vez por sesión HTTP
public class MiBeanDeSesion {
    // Este bean está asociado a la sesión del usuario
}

// @Cacheable: Marca un método que debe almacenar en caché su resultado.
import org.springframework.cache.annotation.Cacheable;

@Cacheable("productos") // El resultado de este método se almacena en la caché bajo la clave 'productos'
public class MiServicioCache {

    public String obtenerProducto(int id) {
        // Simula una operación costosa
        return "Producto " + id;
    }
}

// @CacheEvict: Marca un método que debe eliminar un elemento de la caché.
import org.springframework.cache.annotation.CacheEvict;

@CacheEvict(value = "productos", key = "#id") // Elimina de la caché la clave 'id' del conjunto 'productos'
public void eliminarProducto(int id) {
    // Lógica para eliminar un producto
}

// @EnableTransactionManagement: Habilita el soporte de gestión de transacciones en la aplicación.
import org.springframework.transaction.annotation.EnableTransactionManagement;

@EnableTransactionManagement // Activa la gestión de transacciones en la aplicación
public class ConfiguracionTransacciones {
    // Aquí se pueden definir métodos transaccionales con @Transactional
}

// @Transactional: Marca un método o clase para que se ejecute dentro de una transacción.
import org.springframework.transaction.annotation.Transactional;

@Transactional // Marca el método para que se ejecute dentro de una transacción
public class MiServicioTransacciones {
    
    public void realizarOperacion() {
        // Lógica de negocio que se ejecuta dentro de una transacción
    }
}

// @EnableWebSecurity: Activa la seguridad web en la aplicación.
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;

@EnableWebSecurity // Activa la configuración de seguridad web
public class ConfiguracionSeguridad {
    // Aquí se definen las reglas de seguridad para la aplicación
}

// @EnableAspectJAutoProxy(proxyTargetClass = true): Activa los aspectos con proxies de clases concretas.
import org.springframework.context.annotation.EnableAspectJAutoProxy;

@EnableAspectJAutoProxy(proxyTargetClass = true) // Proxies basados en clases concretas, no interfaces
public class ConfiguracionAOP {
    // Aquí se configuran los aspectos con proxy de clase
}

// @ControllerAdvice: Permite manejar excepciones globales y aplicar lógica antes/después de los métodos de los controladores.
import org.springframework.web.bind.annotation.ControllerAdvice;

@ControllerAdvice // Clase que maneja excepciones globales para los controladores
public class GlobalExcepciones {

    @ExceptionHandler(Exception.class) // Manejador de excepciones global
    public String manejarExcepcion(Exception ex) {
        return "Error: " + ex.getMessage();
    }
}

```
