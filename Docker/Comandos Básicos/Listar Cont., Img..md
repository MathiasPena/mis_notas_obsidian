
En Docker, uno de los aspectos más comunes es visualizar los contenedores e imágenes que están en tu sistema. A continuación, te explico cómo listar contenedores e imágenes, con ejemplos y detalles importantes.

#### **Listar Contenedores**

Puedes listar los contenedores en ejecución o todos los contenedores, incluso los detenidos. Esto se hace con los siguientes comandos:

1. **Listar contenedores en ejecución**:
   
   El comando `docker ps` muestra todos los contenedores que están actualmente en ejecución.

   ```bash
   docker ps
   ```

   Esto te devolverá una lista de contenedores activos, con la siguiente información:

   - **CONTAINER ID**: Un identificador único para cada contenedor.
   - **IMAGE**: La imagen de la que se creó el contenedor.
   - **COMMAND**: El comando que se está ejecutando dentro del contenedor.
   - **CREATED**: Cuánto tiempo hace que se creó el contenedor.
   - **STATUS**: El estado del contenedor (por ejemplo, "Up 5 minutes").
   - **PORTS**: Los puertos que el contenedor ha expuesto.
   - **NAMES**: El nombre del contenedor (puede ser asignado automáticamente o personalizado).

   Ejemplo de salida:

   ```bash
   CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                  NAMES
   7c1f77d1baf0   nginx     "/docker-entrypoint.…"   2 hours ago      Up 2 hours      0.0.0.0:8080->80/tcp   web_server
   ```

2. **Listar todos los contenedores, incluyendo los detenidos**:

   Si deseas ver todos los contenedores, no solo los que están en ejecución, puedes agregar el flag `-a` o `--all` al comando `docker ps`.

   ```bash
   docker ps -a
   ```

   Esto mostrará todos los contenedores en el sistema, tanto los que están corriendo como los detenidos, con la misma información que el comando anterior.

   Ejemplo de salida:

   ```bash
   CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                  PORTS     NAMES
   7c1f77d1baf0   nginx     "/docker-entrypoint.…"   2 hours ago      Up 2 hours              0.0.0.0:8080->80/tcp   web_server
   f1a1d7c68794   ubuntu    "bash"                   3 hours ago      Exited (0) 30 minutes ago            lonely_ubuntu
   ```

#### **Listar Imágenes**

Para listar las imágenes disponibles en tu máquina local, utilizas el comando `docker images` o `docker image ls` (son equivalentes).

```bash
docker images
```

Esto te mostrará una lista de todas las imágenes locales disponibles, con la siguiente información:

- **REPOSITORY**: El nombre de la imagen (por ejemplo, `nginx`, `ubuntu`).
- **TAG**: La etiqueta que identifica una versión específica de la imagen (por ejemplo, `latest`, `1.0`).
- **IMAGE ID**: Un identificador único de la imagen.
- **CREATED**: Cuánto tiempo hace que se creó la imagen.
- **SIZE**: El tamaño de la imagen.

Ejemplo de salida:

```bash
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
nginx          latest    9b7db4efbf1a   2 days ago       133MB
ubuntu         latest    3f9d02eea8e1   4 weeks ago      64.2MB
node           14        99fa35c2a1b0   2 months ago     907MB
```

#### **Opciones útiles para personalizar la salida**

Ambos comandos `docker ps` y `docker images` tienen varias opciones que puedes utilizar para personalizar la salida. Algunas de las más útiles son:

- **Mostrar solo ciertos campos**:

  Si deseas ver solo una columna específica, puedes usar el flag `--format` para formatear la salida.

  Ejemplo: Ver solo los **nombres** de los contenedores:

  ```bash
  docker ps --format "{{.Names}}"
  ```

  Ejemplo: Ver solo los **ID de las imágenes**:

  ```bash
  docker images --format "{{.ID}}"
  ```

- **Filtrar los resultados**:

  Si tienes muchos contenedores o imágenes y deseas filtrar los resultados, puedes usar el flag `--filter` o `-f`.

  Ejemplo: Mostrar solo contenedores que están **detenidos**:

  ```bash
  docker ps -a --filter "status=exited"
  ```

  Ejemplo: Mostrar solo imágenes que contienen la palabra `nginx`:

  ```bash
  docker images --filter "reference=nginx"
  ```

- **Mostrar el historial de una imagen**:

  Puedes ver el historial de una imagen (las capas que contiene) usando el siguiente comando:

  ```bash
  docker history <image_name_or_id>
  ```

  Ejemplo:

  ```bash
  docker history nginx:latest
  ```

#### **Resumen**

Para listar contenedores e imágenes en Docker, puedes utilizar los comandos `docker ps` y `docker images`, que te permiten ver los contenedores y las imágenes que están presentes en tu máquina. Usando flags y filtros adicionales, puedes personalizar y adaptar la salida a tus necesidades.