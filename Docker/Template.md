# Docker - Comandos Básicos y Uso

## 1. Instalación y Verificación
```sh
docker --version
```

## 2. Comandos Esenciales
### Iniciar y detener Docker
```sh
docker start <container_id>
docker stop <container_id>
```

### Listar contenedores
```sh
docker ps              # Contenedores en ejecución
docker ps -a           # Todos los contenedores
```

### Ejecutar un contenedor
```sh
docker run -d --name my_container -p 8080:80 nginx
```

### Acceder a un contenedor
```sh
docker exec -it <container_id> /bin/sh  # o /bin/bash
```

### Eliminar contenedores
```sh
docker rm <container_id>
docker rm $(docker ps -aq)  # Eliminar todos
```

### Ver logs de un contenedor
```sh
docker logs <container_id>
```

---
## 3. Imágenes
### Listar imágenes locales
```sh
docker images
```

### Descargar imágenes
```sh
docker pull ubuntu
```

### Construir una imagen desde un Dockerfile
```sh
docker build -t my_image .
```

### Eliminar imágenes
```sh
docker rmi <image_id>
```

---
## 4. Dockerfile - Creación de Imágenes
Ejemplo básico:
```dockerfile
# Usar una imagen base
FROM python:3.9

# Copiar archivos
COPY . /app

# Definir directorio de trabajo
WORKDIR /app

# Instalar dependencias
RUN pip install -r requirements.txt

# Definir el comando por defecto
CMD ["python", "app.py"]
```

Construcción y ejecución:
```sh
docker build -t my_python_app .
docker run -d -p 5000:5000 my_python_app
```

---
## 5. Docker Compose (Múltiples Contenedores)
Ejemplo `docker-compose.yml`:
```yaml
version: '3.8'
services:
  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
  app:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - db
```
Ejecutar:
```sh
docker-compose up -d
docker-compose down
```

### 3.3 **Ejecutar un contenedor**
```bash
# Ejecutar un contenedor de Nginx
docker run -d -p 80:80 nginx
```


### 3.10 **Acceder a la terminal de un contenedor**
```bash
docker exec -it <container_id> /bin/bash
```

---

## 4. **Dockerfile**

### 4.1 **¿Qué es un Dockerfile?**
Un Dockerfile es un archivo de texto que contiene instrucciones que Docker sigue para construir una imagen. Cada instrucción en un Dockerfile crea una capa en la imagen.

### 4.2 **Estructura Básica de un Dockerfile**
```dockerfile
# Seleccionamos una imagen base
FROM ubuntu:20.04

# Mantenedor de la imagen
LABEL maintainer="tu_email@dominio.com"

# Instalamos dependencias
RUN apt-get update && apt-get install -y python3 python3-pip

# Copiar archivos al contenedor
COPY ./mi_app /app

# Establecer el directorio de trabajo
WORKDIR /app

# Exponer puertos
EXPOSE 8080

# Comando para ejecutar la aplicación
CMD ["python3", "app.py"]
```

### 4.3 **Instrucciones Comunes en un Dockerfile**
- **FROM**: Define la imagen base. Ejemplo: `FROM ubuntu:20.04`.
- **RUN**: Ejecuta comandos dentro del contenedor. Ejemplo: `RUN apt-get update && apt-get install -y python3`.
- **COPY**: Copia archivos desde el host al contenedor. Ejemplo: `COPY ./mi_app /app`.
- **WORKDIR**: Establece el directorio de trabajo dentro del contenedor. Ejemplo: `WORKDIR /app`.
- **EXPOSE**: Expone puertos a través del contenedor. Ejemplo: `EXPOSE 8080`.
- **CMD**: Define el comando por defecto que se ejecuta al iniciar el contenedor. Ejemplo: `CMD ["python3", "app.py"]`.
- **ENTRYPOINT**: Similar a CMD pero no se puede sobrescribir. Ejemplo: `ENTRYPOINT ["python3", "app.py"]`.
- **VOLUME**: Crea un punto de montaje para almacenamiento persistente. Ejemplo: `VOLUME /data`.

### 4.4 **Ejemplo Completo de Dockerfile**
```dockerfile
# Usar una imagen base de Node.js
FROM node:14

# Crear y establecer el directorio de trabajo
WORKDIR /usr/src/app

# Copiar los archivos de la aplicación al contenedor
COPY package*.json ./
RUN npm install
COPY . .

# Exponer el puerto que la aplicación usará
EXPOSE 8080

# Comando para iniciar la aplicación
CMD ["node", "app.js"]
```

---

## 5. **Construir y Etiquetar Imágenes**

### 5.1 **Construir una Imagen**
```bash
docker build -t nombre_imagen .
```

### 5.2 **Construir con Etiqueta (Tag)**
```bash
docker build -t nombre_imagen:v1 .
```

### 5.3 **Listar Imágenes**
```bash
docker images
```

---

## 6. **Correr Contenedores**

### 6.1 **Ejecutar un Contenedor con un Puerto Expuesto**
```bash
docker run -d -p 8080:8080 nombre_imagen
```

### 6.2 **Ejecutar un Contenedor Interactivo**
```bash
docker run -it nombre_imagen /bin/bash
```

### 6.3 **Ejecutar un Contenedor y Detenerlo**
```bash
docker run --rm nombre_imagen
```

### 6.4 **Conectar un Contenedor a una Red**
```bash
docker network create mi_red
docker run -d --net mi_red nombre_imagen
```

---

## 7. **Docker Compose**

### 7.1 **¿Qué es Docker Compose?**
Docker Compose es una herramienta para definir y ejecutar aplicaciones multicontenedor. Usas un archivo `docker-compose.yml` para configurar los contenedores, redes y volúmenes.

### 7.2 **Estructura Básica de `docker-compose.yml`**
```yaml
version: '3'
services:
  app:
    image: nombre_imagen
    ports:
      - "8080:8080"
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: ejemplo
    volumes:
      - db_data:/var/lib/mysql
volumes:
  db_data:
```

### 7.3 **Comandos Comunes de Docker Compose**
- **Iniciar todos los contenedores definidos en el archivo `docker-compose.yml`**:
  ```bash
  docker-compose up
  ```

- **Iniciar en segundo plano**:
  ```bash
  docker-compose up -d
  ```

- **Detener los contenedores**:
  ```bash
  docker-compose down
  ```

---

## 8. **Volúmenes y Persistencia de Datos**

### 8.1 **Crear un Volumen**
```bash
docker volume create nombre_volumen
```

### 8.2 **Montar un Volumen en un Contenedor**
```bash
docker run -d -v nombre_volumen:/data nombre_imagen
```

### 8.3 **Ver Volúmenes**
```bash
docker volume ls
```

### 8.4 **Eliminar Volúmenes**
```bash
docker volume rm nombre_volumen
```

---

## 9. **Redes en Docker**

### 9.1 **Crear una Red de Contenedores**
```bash
docker network create mi_red
```

### 9.2 **Conectar un Contenedor a una Red**
```bash
docker run -d --net mi_red nombre_imagen
```

### 9.3 **Listar Redes**
```bash
docker network ls
```

---

## 10. **Manejo de Logs**

### 10.1 **Ver los Logs de un Contenedor**
```bash
docker logs <container_id>
```

### 10.2 **Ver los Logs en Tiempo Real**
```bash
docker logs -f <container_id>
```

---

## 11. **Consideraciones de Seguridad**

### 11.1 **Permisos de Contenedores**
- Evita ejecutar contenedores con privilegios innecesarios.
- Usa imágenes oficiales siempre que sea posible.
- Asegúrate de configurar correctamente los puertos expuestos.

### 11.2 **Escaneo de Vulnerabilidades**
- Usa herramientas como `Docker scan` para analizar vulnerabilidades en las imágenes.

```bash
docker scan nombre_imagen
```

---

## 12. **Optimización de Imágenes**

### 12.1 **Usar Imágenes Base Más Livianas**
Utiliza imágenes base pequeñas como `alpine` para reducir el tamaño de la imagen.

```dockerfile
FROM node:14-alpine
```

### 12.2 **Eliminar Cachés y Archivos No Necesarios**
En el Dockerfile, usa `RUN apt-get clean` o elimina archivos temporales después de instalar dependencias.

---

Este template cubre desde lo básico hasta algunos aspectos más avanzados para gestionar contenedores y optimizar imágenes. Puedes adaptarlo según tus necesidades y proyectos.
