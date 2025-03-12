
Docker usa imágenes para crear contenedores. Las imágenes son plantillas inmutables de software que contienen todo lo necesario para ejecutar una aplicación, como el código, las librerías y el sistema operativo. Aquí te muestro cómo gestionar las imágenes en Docker, desde su creación hasta su eliminación.

#### **Ver las imágenes disponibles**

Para ver las imágenes que tienes descargadas localmente, puedes usar el siguiente comando:

```bash
docker images
```

Este comando te dará una lista de las imágenes locales, mostrando información como el nombre de la imagen, la etiqueta (tag), el ID, el tamaño y la fecha de creación.

**Ejemplo de salida:**

```bash
REPOSITORY          TAG       IMAGE ID       CREATED          SIZE
nginx               latest    d1d1d1d1d1d1   2 weeks ago      132MB
ubuntu              20.04     2d2d2d2d2d2d   3 months ago     64MB
```

#### **Buscar imágenes en Docker Hub**

Si necesitas una imagen que no tienes localmente, puedes buscarla en Docker Hub usando el comando `docker search`:

```bash
docker search <image_name>
```

**Ejemplo:**

```bash
docker search nginx
```

Este comando buscará imágenes relacionadas con `nginx` en Docker Hub.

#### **Descargar una imagen**

Para descargar una imagen de Docker Hub, usa el comando `docker pull`. Si no especificas una etiqueta (tag), Docker descargará la última versión (`latest`):

```bash
docker pull <image_name>:<tag>
```

**Ejemplo:**

```bash
docker pull nginx:latest
```

Este comando descargará la última versión de la imagen de `nginx` desde Docker Hub.

#### **Crear una imagen a partir de un contenedor**

Puedes crear una imagen a partir de un contenedor que ya está en ejecución. Esto es útil si has hecho cambios en un contenedor y quieres guardarlos como una nueva imagen.

Para crear una imagen a partir de un contenedor, usa el comando `docker commit`:

```bash
docker commit <container_id> <new_image_name>:<tag>
```

**Ejemplo:**

```bash
docker commit d5d2e0a1f2f7 mi_imagen_nginx:1.0
```

Este comando creará una nueva imagen llamada `mi_imagen_nginx` con la etiqueta `1.0` a partir del contenedor `d5d2e0a1f2f7`.

#### **Etiquetar una imagen**

Si tienes una imagen y quieres cambiar su etiqueta (tag), puedes usar el comando `docker tag`:

```bash
docker tag <image_id> <new_image_name>:<new_tag>
```

**Ejemplo:**

```bash
docker tag d1d1d1d1d1d1 mi_imagen_nginx:v1.0
```

Este comando creará una nueva etiqueta `v1.0` para la imagen `mi_imagen_nginx`.

#### **Eliminar una imagen**

Si ya no necesitas una imagen, puedes eliminarla usando el comando `docker rmi`:

```bash
docker rmi <image_id>
```

**Ejemplo:**

```bash
docker rmi d1d1d1d1d1d1
```

Este comando eliminará la imagen con ID `d1d1d1d1d1d1`. Si la imagen está siendo utilizada por algún contenedor, primero tendrás que detener y eliminar ese contenedor.

#### **Eliminar varias imágenes**

Si deseas eliminar varias imágenes a la vez, puedes pasar varios IDs de imagen al comando `rmi`:

```bash
docker rmi <image_id1> <image_id2>
```

**Ejemplo:**

```bash
docker rmi d1d1d1d1d1d1 d2d2d2d2d2d2
```

Este comando eliminará las imágenes con los IDs especificados.

#### **Eliminar imágenes no utilizadas**

Si deseas eliminar todas las imágenes que no están siendo utilizadas por ningún contenedor, puedes usar el siguiente comando:

```bash
docker image prune
```

Esto eliminará todas las imágenes "colgadas" que no tienen contenedores asociados.

#### **Resumen de Comandos para Gestionar Imágenes:**

| Comando                        | Descripción                                               |
|---------------------------------|-----------------------------------------------------------|
| `docker images`                 | Ver las imágenes locales.                                |
| `docker search <image_name>`    | Buscar imágenes en Docker Hub.                            |
| `docker pull <image_name>`      | Descargar una imagen desde Docker Hub.                    |
| `docker commit <container_id> <new_image_name>` | Crear una imagen desde un contenedor.                    |
| `docker tag <image_id> <new_image_name>:<new_tag>` | Etiquetar una imagen con un nuevo tag.                    |
| `docker rmi <image_id>`         | Eliminar una imagen.                                      |
| `docker rmi <image_id1> <image_id2>` | Eliminar varias imágenes a la vez.                         |
| `docker image prune`            | Eliminar imágenes no utilizadas.                          |

#### **Verificación de Espacio Utilizado por Imágenes**

Si deseas ver cuánto espacio están ocupando las imágenes y contenedores, puedes usar:

```bash
docker system df
```

Este comando mostrará estadísticas de espacio utilizadas por las imágenes, contenedores, volúmenes, etc.

