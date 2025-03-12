
Una de las tareas más comunes con Docker es ejecutar contenedores a partir de imágenes. Esto te permite aislar aplicaciones y sus dependencias dentro de contenedores que son fácilmente reproducibles y transportables.

#### **Ejecutar un contenedor**

Para ejecutar un contenedor, usas el comando `docker run`, seguido de la imagen que deseas usar. Este comando descargará la imagen (si no está disponible localmente) y ejecutará el contenedor.

**Sintaxis básica:**

```bash
docker run [opciones] <imagen> [comando]
```

#### **Ejemplo básico:**

Ejecutar un contenedor con la imagen de `nginx`:

```bash
docker run nginx
```

Este comando hace lo siguiente:
- Docker buscará la imagen `nginx` en tu máquina local.
- Si no la encuentra, la descargará desde Docker Hub.
- Luego, ejecutará la imagen en un contenedor de manera predeterminada, lo que iniciará el servicio `nginx` dentro del contenedor.

**Salida esperada**:

El contenedor se ejecutará en segundo plano (detenido), a menos que le especifiques puertos o interactúes con él.

#### **Ejecutar contenedor en segundo plano (detached mode)**

Si deseas que el contenedor se ejecute en segundo plano, puedes usar la opción `-d` (detached mode). Esto es útil cuando no necesitas interactuar con el contenedor directamente, pero aún quieres que esté en funcionamiento.

```bash
docker run -d nginx
```

Este comando ejecutará `nginx` en segundo plano y devolverá el ID del contenedor.

#### **Asignar puertos a un contenedor**

Es común ejecutar aplicaciones web dentro de un contenedor, y en ese caso, necesitas exponer puertos para que el contenedor pueda ser accesible desde tu máquina local. Para hacer esto, usa la opción `-p` para mapear los puertos del contenedor al host.

**Sintaxis**:

```bash
docker run -p <puerto_host>:<puerto_contenedor> <imagen>
```

**Ejemplo:**

```bash
docker run -d -p 8080:80 nginx
```

En este caso:
- `-d` ejecuta el contenedor en segundo plano.
- `-p 8080:80` mapea el puerto 8080 de tu máquina local al puerto 80 dentro del contenedor.
- Así, puedes acceder a la aplicación `nginx` ejecutándose dentro del contenedor abriendo tu navegador y dirigiéndote a `http://localhost:8080`.

#### **Nombrar un contenedor**

Puedes darle un nombre personalizado al contenedor con la opción `--name`.

```bash
docker run -d --name mi_nginx -p 8080:80 nginx
```

Con esto, el contenedor se llamará `mi_nginx` en lugar de generar un nombre aleatorio.

#### **Ejecutar un contenedor con un comando específico**

Al ejecutar un contenedor, puedes especificar qué comando ejecutar dentro de él. Por defecto, las imágenes tienen un comando predefinido (como iniciar un servidor web o shell). Si deseas ejecutar algo diferente, simplemente añades el comando al final de la instrucción.

**Ejemplo: Ejecutar un contenedor de `ubuntu` y abrir una terminal interactiva (bash)**:

```bash
docker run -it ubuntu bash
```

- `-i` mantiene la entrada estándar (stdin) abierta para que puedas interactuar con el contenedor.
- `-t` asigna un terminal al contenedor.
- `bash` es el comando que se ejecutará dentro del contenedor (en este caso, abrirá una terminal de Bash).

Ahora estarás dentro del contenedor `ubuntu` y podrás ejecutar comandos como si estuvieras en una máquina normal.

#### **Montar volúmenes (volumes)**

Si deseas que los cambios realizados dentro del contenedor persistan incluso después de que el contenedor se detenga o se elimine, puedes montar un volumen. Los volúmenes permiten compartir archivos entre el contenedor y tu máquina local.

**Sintaxis**:

```bash
docker run -v <directorio_local>:<directorio_contenedor> <imagen>
```

**Ejemplo:**

```bash
docker run -d -v /mi/directorio/local:/var/www/html nginx
```

Este comando montará el directorio local `/mi/directorio/local` dentro del contenedor en la ruta `/var/www/html`. Los cambios que realices en esa carpeta local se reflejarán dentro del contenedor y viceversa.

#### **Limitar recursos al contenedor**

Docker te permite limitar los recursos que un contenedor puede usar, como la CPU y la memoria. Esto puede ser útil para evitar que un contenedor consuma demasiados recursos en el sistema.

**Ejemplo: Limitar la memoria a 100MB y la CPU a 0.5 núcleos:**

```bash
docker run -d --memory="100m" --cpus="0.5" nginx
```

Este comando limitará el contenedor a 100MB de RAM y 0.5 de CPU.

#### **Ejecutar contenedores con variables de entorno**

Puedes pasar variables de entorno al contenedor durante su ejecución. Esto es útil para configurar aplicaciones sin necesidad de modificar el código fuente o los archivos de configuración.

**Ejemplo:**

```bash
docker run -d -e "MY_ENV_VAR=valor" nginx
```

Este comando pasará la variable de entorno `MY_ENV_VAR` con el valor `valor` al contenedor de `nginx`.

#### **Ejecutar contenedor interactivo con un volumen**

Si deseas ejecutar un contenedor interactivo y montar un volumen para compartir archivos, el comando sería el siguiente:

```bash
docker run -it -v /mi/directorio/local:/data ubuntu bash
```

Esto te permitirá interactuar con el contenedor y tener acceso a los archivos dentro de `/mi/directorio/local` que estarán disponibles en `/data` dentro del contenedor.

#### **Resumen de opciones comunes al ejecutar contenedores:**

| Opción               | Descripción                                           |
|----------------------|-------------------------------------------------------|
| `-d`                 | Ejecutar el contenedor en segundo plano (detached).   |
| `-p`                 | Mapear puertos del contenedor al host (host:container).|
| `-it`                | Ejecutar contenedor interactivo (stdin y terminal).   |
| `--name`             | Asignar un nombre personalizado al contenedor.        |
| `-v`                 | Montar un volumen (directorio compartido entre el contenedor y el host).|
| `--memory`           | Limitar la memoria del contenedor.                    |
| `--cpus`             | Limitar la cantidad de CPU del contenedor.            |
| `-e`                 | Pasar variables de entorno al contenedor.             |

#### **Ejemplo de ejecución completo:**

```bash
docker run -d -p 8080:80 --name mi_web -v /mi/directorio/local:/var/www/html nginx
```

Este comando:
- Ejecuta `nginx` en segundo plano (`-d`).
- Mapea el puerto 8080 del host al puerto 80 del contenedor.
- Asigna el nombre `mi_web` al contenedor.
- Monta el directorio local `/mi/directorio/local` al contenedor en `/var/www/html`.

Con estos ejemplos y opciones, deberías tener una buena comprensión de cómo ejecutar contenedores en Docker, adaptándolos a diferentes necesidades.

