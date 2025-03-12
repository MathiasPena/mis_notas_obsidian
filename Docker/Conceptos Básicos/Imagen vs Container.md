
En Docker, las **imágenes** y los **contenedores** son conceptos clave, pero tienen diferencias importantes en su funcionamiento y en cómo se utilizan.

#### **¿Qué es una Imagen Docker?**

Una **imagen Docker** es un archivo inmutable que contiene todo lo necesario para ejecutar una aplicación: código, bibliotecas, dependencias, configuraciones y todo lo que necesita el sistema para ejecutar una aplicación en particular. Las imágenes se construyen a partir de un **Dockerfile**, que es un conjunto de instrucciones para construir la imagen.

**Características de las Imágenes Docker:**

- **Inmutables**: Una vez que se crea una imagen, no se puede modificar. Cualquier cambio que se desee hacer debe ser hecho a través de la creación de una nueva imagen.
- **Capas**: Las imágenes están compuestas por múltiples capas que se crean en función de las instrucciones del Dockerfile. Cada capa es una modificación sobre la capa anterior, y Docker usa un sistema de almacenamiento eficiente para compartir estas capas entre diferentes imágenes.
- **Portabilidad**: Las imágenes son portátiles y pueden ser ejecutadas en cualquier máquina que tenga Docker instalado. Esto garantiza que una aplicación funcione de la misma manera en diferentes entornos.
- **Docker Hub**: Las imágenes se pueden almacenar y compartir a través de Docker Hub, que es un registro centralizado donde puedes encontrar imágenes oficiales, como las de **nginx**, **mysql**, **node** y muchas más.

##### **Cómo crear una imagen:**

Para crear una imagen, se utiliza el comando `docker build` junto con un Dockerfile. Este archivo especifica cómo debe construirse la imagen y qué pasos seguir. Aquí tienes un ejemplo simple de un Dockerfile:

```Dockerfile
# Utiliza una imagen base oficial de Node.js
FROM node:14

# Establece el directorio de trabajo
WORKDIR /app

# Copia los archivos del proyecto al contenedor
COPY . .

# Instala las dependencias
RUN npm install

# Expone el puerto que va a escuchar la aplicación
EXPOSE 3000

# Comando para ejecutar la aplicación
CMD ["npm", "start"]
```

Este archivo `Dockerfile` describe cómo crear una imagen que contenga una aplicación Node.js. El comando `docker build` usará este Dockerfile para construir la imagen.

#### **¿Qué es un Contenedor Docker?**

Un **contenedor Docker** es una instancia en ejecución de una imagen Docker. Cuando se ejecuta una imagen, Docker crea un contenedor que es aislado, pero que tiene acceso a los recursos del sistema operativo subyacente. Un contenedor es como un proceso en ejecución en el sistema, pero está aislado de otros procesos y entornos.

**Características de los Contenedores Docker:**

- **Instancia en ejecución**: Un contenedor es una instancia en ejecución de una imagen. Mientras que la imagen es estática, un contenedor es dinámico y se puede iniciar, detener, reiniciar y eliminar.
- **Volatilidad**: Los contenedores son volátiles. Cuando un contenedor se elimina, sus datos (a menos que se usen volúmenes) también se eliminan. Sin embargo, las imágenes son persistentes y no se pierden al eliminar un contenedor.
- **Aislamiento**: Aunque los contenedores comparten el mismo kernel del sistema operativo, están aislados entre sí. Esto significa que un contenedor no puede interferir con otro contenedor o con el sistema operativo host, aunque comparten recursos como el CPU y la memoria.
- **Efímeros**: Un contenedor puede ser detenido y eliminado fácilmente. Cuando se detiene un contenedor, se puede volver a iniciar sin perder sus configuraciones y datos, si se han configurado correctamente.

##### **Comandos básicos para trabajar con contenedores:**

- **Crear un contenedor**: 

    ```bash
    docker run -d --name my-container my-image
    ```

    Este comando ejecuta un contenedor a partir de la imagen `my-image` en modo desacoplado (`-d`), asignándole el nombre `my-container`.

- **Ver los contenedores en ejecución**:

    ```bash
    docker ps
    ```

    Muestra los contenedores activos en el sistema.

- **Detener un contenedor**:

    ```bash
    docker stop my-container
    ```

    Detiene el contenedor llamado `my-container`.

- **Eliminar un contenedor**:

    ```bash
    docker rm my-container
    ```

    Elimina el contenedor `my-container` del sistema.

#### **Diferencias clave entre imágenes y contenedores:**

| Característica             | Imagen Docker                              | Contenedor Docker                         |
|----------------------------|--------------------------------------------|-------------------------------------------|
| **Definición**              | Plantilla que contiene el código y dependencias necesarias para ejecutar una aplicación | Instancia en ejecución de una imagen      |
| **Inmutabilidad**           | Inmutable, no puede cambiarse una vez creada | Mutable, puedes iniciar, detener y eliminar contenedores |
| **Estado**                  | No tiene estado de ejecución               | Tiene un estado de ejecución (corriendo, detenido) |
| **Propósito**               | Crear y almacenar aplicaciones y sus dependencias | Ejecutar aplicaciones empaquetadas en una imagen |
| **Persistencia**            | Persistente a través de reconstrucciones y comparticiones | No persistente, se pierde al eliminar el contenedor |
| **Ubicación**               | Se almacena como archivo o en un registro (Docker Hub) | Se ejecuta en el sistema operativo del host |

#### **Resumen:**

- Una **imagen Docker** es un archivo estático que contiene todo lo necesario para ejecutar una aplicación.
- Un **contenedor Docker** es una instancia en ejecución de una imagen, proporcionando un entorno aislado y controlado para que la aplicación se ejecute.

