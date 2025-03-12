

El módulo `logging` de Python proporciona una forma flexible y eficiente de registrar mensajes durante la ejecución de un programa. Es útil para depuración, monitoreo y análisis de aplicaciones, permitiendo gestionar niveles de log, diferentes destinos y formatos.

### 🛠️ Configuración Básica del Logging

El módulo `logging` ofrece varias configuraciones, que incluyen niveles de severidad, **handlers** para destinos (como archivos o consola), y **formatters** para definir cómo se muestra el log.

#### 1.1. **Niveles de Log**

Los niveles de log permiten filtrar los mensajes registrados según su importancia. Los niveles estándar son:

- **DEBUG**: Información detallada, generalmente solo útil durante el desarrollo.
- **INFO**: Información general sobre la ejecución del programa.
- **WARNING**: Advertencias que no detienen la ejecución, pero podrían indicar un problema.
- **ERROR**: Errores que afectan el flujo del programa, pero no detienen la ejecución.
- **CRITICAL**: Errores graves que generalmente causan la terminación del programa.

#### 1.2. **Configuración Básica de Logging**

```python
import logging

# Configuración básica
logging.basicConfig(level=logging.INFO)

logging.debug("Este es un mensaje de depuración")
logging.info("Este es un mensaje informativo")
logging.warning("Este es un mensaje de advertencia")
logging.error("Este es un mensaje de error")
logging.critical("Este es un mensaje crítico")
```

Este código imprime todos los mensajes con nivel `INFO` o superior. El `level=logging.INFO` indica que solo se registrarán mensajes con nivel `INFO`, `WARNING`, `ERROR` y `CRITICAL`.

---

### 🛠️ Handlers

Los **handlers** son responsables de enviar los mensajes de log a su destino adecuado, como archivos, la consola o incluso servidores remotos.

#### 2.1. **StreamHandler (Consola)**

Envía los logs a la salida estándar (como la consola).

```python
import logging

# Crear un logger
logger = logging.getLogger('mi_logger')

# Crear un handler para la consola
console_handler = logging.StreamHandler()

# Establecer el formato del log
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
console_handler.setFormatter(formatter)

# Añadir el handler al logger
logger.addHandler(console_handler)

# Registrar un mensaje
logger.info("Este es un log en la consola")
```

#### 2.2. **FileHandler (Archivo)**

Envía los logs a un archivo, permitiendo registrar los mensajes en un archivo de texto.

```python
import logging

# Crear un logger
logger = logging.getLogger('mi_logger')

# Crear un handler para el archivo
file_handler = logging.FileHandler('mi_log.txt')

# Establecer el formato del log
formatter = logging.Formatter('%(asctime)s - %(levelname)s - %(message)s')
file_handler.setFormatter(formatter)

# Añadir el handler al logger
logger.addHandler(file_handler)

# Registrar un mensaje
logger.error("Este es un log en un archivo")
```

#### 2.3. **RotatingFileHandler (Rotación de Archivos)**

El `RotatingFileHandler` permite rotar los archivos de log cuando alcanzan un tamaño máximo, creando nuevos archivos de log.

```python
import logging
from logging.handlers import RotatingFileHandler

# Crear un logger
logger = logging.getLogger('mi_logger')

# Crear un handler para la rotación de archivos
rotating_handler = RotatingFileHandler('mi_log_rotado.txt', maxBytes=2000, backupCount=5)

# Establecer el formato del log
formatter = logging.Formatter('%(asctime)s - %(levelname)s - %(message)s')
rotating_handler.setFormatter(formatter)

# Añadir el handler al logger
logger.addHandler(rotating_handler)

# Registrar un mensaje
logger.warning("Este es un log con rotación de archivo")
```

---

### 🛠️ Formatters

Los **formatters** definen el formato de los mensajes de log. Puedes incluir información como la fecha, hora, nivel de log, el mensaje, el archivo desde el cual se originó el log, etc.

#### 3.1. **Formato Básico**

```python
import logging

# Crear un logger
logger = logging.getLogger('mi_logger')

# Crear un handler para la consola
console_handler = logging.StreamHandler()

# Establecer el formato del log
formatter = logging.Formatter('%(asctime)s - %(levelname)s - %(message)s')
console_handler.setFormatter(formatter)

# Añadir el handler al logger
logger.addHandler(console_handler)

# Registrar un mensaje
logger.debug("Este es un mensaje con formato")
```

#### 3.2. **Formato Completo**

Se puede incluir más información en el formato, como el nombre del archivo, la línea de código y el nombre del logger.

```python
import logging

# Crear un logger
logger = logging.getLogger('mi_logger')

# Crear un handler para la consola
console_handler = logging.StreamHandler()

# Formato detallado
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s - %(filename)s - %(lineno)d')
console_handler.setFormatter(formatter)

# Añadir el handler al logger
logger.addHandler(console_handler)

# Registrar un mensaje
logger.error("Este es un mensaje con formato detallado")
```

---

### 🚀 Conclusión

El módulo `logging` de Python es una herramienta poderosa para crear registros detallados de las actividades del programa, lo cual es crucial para la depuración, monitoreo y mantenimiento. Al combinar niveles de log, handlers para múltiples destinos y formatters para personalizar la salida, puedes gestionar de manera eficiente cómo se registran y almacenan los mensajes. Siguiendo estas buenas prácticas, podrás tener un registro más organizado y útil en tus aplicaciones.
