
Un `Dockerfile` es un archivo de texto que contiene una serie de instrucciones que Docker utiliza para crear una imagen personalizada. Cada instrucción en un `Dockerfile` crea una capa en la imagen resultante, y cada capa está construida sobre la anterior.

La estructura básica de un `Dockerfile` incluye una serie de instrucciones que se ejecutan en orden secuencial para crear la imagen. La mayoría de los archivos `Dockerfile` siguen una estructura estándar y modular.

#### **Estructura básica de un Dockerfile:**

```dockerfile
# Instrucción 1: Especificar la imagen base
FROM <imagen_base>

# Instrucción 2: Establecer variables de entorno
ENV <nombre_variable> <valor>

# Instrucción 3: Crear directorios dentro del contenedor
RUN mkdir /app

# Instrucción 4: Copiar archivos desde el sistema local al contenedor
COPY <ruta_local> <ruta_contenedor>

# Instrucción 5: Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# Instrucción 6: Instalar dependencias o ejecutar comandos
RUN apt-get update && apt-get install -y <paquete>

# Instrucción 7: Exponer puertos
EXPOSE 80

# Instrucción 8: Especificar el comando por defecto a ejecutar cuando se ejecute el contenedor
CMD ["python", "app.py"]
```

#### **Explicación de cada parte de la estructura:**

- **FROM <imagen_base>:**  
  La primera instrucción en un `Dockerfile` es `FROM`, que especifica la imagen base que se usará para crear la nueva imagen. Por ejemplo, puedes usar una imagen oficial de Python, Node.js o Ubuntu.
  
  **Ejemplo:**
  ```dockerfile
  FROM python:3.9-slim
  ```

- **ENV \<nombre_variable\> \<valor\>**
  La instrucción `ENV` se utiliza para establecer variables de entorno dentro del contenedor. Estas variables pueden ser utilizadas por el sistema o las aplicaciones dentro del contenedor.
  
  **Ejemplo:**
  ```dockerfile
  ENV APP_ENV=production
  ```

- **RUN \<comando\>**  
  `RUN` se utiliza para ejecutar comandos dentro de la imagen durante el proceso de construcción. Es comúnmente utilizado para instalar paquetes, actualizar el sistema o realizar configuraciones necesarias.
  
  **Ejemplo:**
  ```dockerfile
  RUN apt-get update && apt-get install -y curl
  ```

- **COPY <ruta_local> <ruta_contenedor>:**  
  `COPY` se utiliza para copiar archivos y directorios desde el sistema local al contenedor. Es ideal para copiar archivos de tu proyecto o código fuente.
  
  **Ejemplo:**
  ```dockerfile
  COPY . /app
  ```

- **WORKDIR \<directorio\>:**  
  La instrucción `WORKDIR` establece el directorio de trabajo dentro del contenedor. Las instrucciones siguientes, como `RUN`, `CMD`, `COPY`, se ejecutarán desde este directorio.
  
  **Ejemplo:**
  ```dockerfile
  WORKDIR /app
  ```

- **EXPOSE \<puerto\>:**  
  `EXPOSE` informa a Docker que el contenedor escuchará en un puerto específico durante su ejecución. No expone el puerto de manera activa, sino que es solo una "notificación" para otros servicios y herramientas que el contenedor necesita ese puerto.
  
  **Ejemplo:**
  ```dockerfile
  EXPOSE 8080
  ```

- **CMD \[comando\]:**  
  `CMD` se usa para especificar el comando predeterminado que se ejecutará cuando el contenedor se inicie. Si el contenedor recibe un comando al iniciarse, reemplazará este comando por el que se pase. Generalmente se usa para iniciar un servicio o aplicación.
  
  **Ejemplo:**
  ```dockerfile
  CMD ["python", "app.py"]
  ```

#### **Otros puntos a considerar sobre Dockerfile:**

- El `Dockerfile` puede contener comentarios usando el símbolo `#`. Los comentarios no son procesados y son solo para mantener la documentación.
  
  **Ejemplo:**
  ```dockerfile
  # Esto es un comentario
  ```

- Un `Dockerfile` debe estar ubicado en la raíz del directorio de tu proyecto o en un lugar que tenga acceso a los archivos que quieres incluir en la imagen.

- Las instrucciones en el `Dockerfile` se ejecutan en orden secuencial. Por ejemplo, si necesitas instalar dependencias antes de copiar el código, debes colocar `RUN` antes de `COPY`.

#### **Ejemplo completo de Dockerfile para una aplicación web simple:**

```dockerfile
# 1. Seleccionar la imagen base
FROM python:3.9-slim

# 2. Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# 3. Copiar el código fuente de la aplicación al contenedor
COPY . /app

# 4. Instalar las dependencias
RUN pip install --no-cache-dir -r requirements.txt

# 5. Exponer el puerto de la aplicación
EXPOSE 5000

# 6. Establecer el comando por defecto para iniciar la aplicación
CMD ["python", "app.py"]
```

### Resumen de instrucciones más comunes:

| Instrucción   | Descripción |
|----------------|-------------|
| `FROM`         | Especifica la imagen base. |
| `ENV`          | Establece variables de entorno. |
| `RUN`          | Ejecuta comandos durante la construcción. |
| `COPY`         | Copia archivos del host al contenedor. |
| `WORKDIR`      | Establece el directorio de trabajo. |
| `EXPOSE`       | Informa sobre puertos que se van a utilizar. |
| `CMD`          | Establece el comando por defecto para ejecutar. |

