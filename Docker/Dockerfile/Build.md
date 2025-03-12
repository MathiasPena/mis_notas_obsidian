
Una vez que tengas tu `Dockerfile` listo, el siguiente paso es construir la imagen utilizando el comando `docker build`. Este comando toma como entrada el `Dockerfile` y produce una imagen Docker personalizada. Puedes agregarle un nombre y un tag a la imagen para facilitar su gestión.

#### **Sintaxis:**
```bash
docker build -t <nombre>:<tag> .
```
- **`<nombre>`**: El nombre que le das a la imagen.
- **`<tag>`**: (Opcional) Una etiqueta para identificar la versión de la imagen (por defecto es `latest`).
- El `.` al final indica que el contexto de la construcción (los archivos que se usarán para construir la imagen) está en el directorio actual.

#### **Ejemplo básico:**
```bash
docker build -t myapp:latest .
```
Este comando crea una imagen llamada `myapp` con la etiqueta `latest` (la etiqueta por defecto). El `.` al final indica que el `Dockerfile` y los archivos necesarios para construir la imagen están en el directorio actual.

#### **Proceso de construcción:**
Cuando ejecutas el comando `docker build`, Docker leerá el `Dockerfile` y ejecutará los pasos de construcción en el orden en que están escritos. Cada instrucción del `Dockerfile` (como `RUN`, `COPY`, etc.) creará una nueva capa en la imagen. Docker optimiza las construcciones reutilizando las capas que no han cambiado.

- **Docker construye en capas**: Cada comando en el `Dockerfile` genera una capa que Docker puede almacenar en caché. Si modificas una capa en tu `Dockerfile`, solo se reconstruirán las capas afectadas y sus dependencias, lo que hace que la construcción sea más eficiente.

#### **Ejemplo con un `Dockerfile` básico:**

Supongamos que tienes el siguiente `Dockerfile` en el directorio actual:

```dockerfile
# Usa la imagen oficial de Node.js como base
FROM node:14

# Establece el directorio de trabajo
WORKDIR /app

# Copia los archivos del proyecto al contenedor
COPY . .

# Instala las dependencias
RUN npm install

# Expone el puerto 3000
EXPOSE 3000

# Comando por defecto al iniciar el contenedor
CMD ["npm", "start"]
```

Para construir la imagen de este `Dockerfile`, usarías:

```bash
docker build -t mynodeapp:1.0 .
```

Este comando:
1. Utiliza `node:14` como base.
2. Copia todos los archivos del proyecto dentro del contenedor.
3. Instala las dependencias del proyecto usando `npm install`.
4. Expone el puerto `3000`.
5. Ejecuta `npm start` cuando el contenedor se inicie.

#### **Ver el progreso de la construcción:**

Cuando ejecutas `docker build`, verás una salida detallada que muestra cómo Docker está construyendo la imagen, incluyendo las capas que está creando. Cada línea del `Dockerfile` se ejecuta y muestra un mensaje como `Step 1/6` para indicar el paso actual.

```bash
Step 1/6 : FROM node:14
 ---> 2d3d1e8e2b4d
Step 2/6 : WORKDIR /app
 ---> Running in 5e5d3d5e64f8
Step 3/6 : COPY . .
 ---> 5b58f9bbd354
Step 4/6 : RUN npm install
 ---> Running in 5abcf5d4d3d3
Step 5/6 : EXPOSE 3000
 ---> Running in 4bc3f3f4d4f4
Step 6/6 : CMD ["npm", "start"]
 ---> Running in 0dfcf9dfd6d6
Successfully built 0dfcf9dfd6d6
Successfully tagged mynodeapp:1.0
```

#### **Ver las imágenes construidas:**

Una vez que hayas construido la imagen, puedes listar las imágenes disponibles en tu máquina usando el siguiente comando:

```bash
docker images
```

Este comando te mostrará una lista de todas las imágenes en tu sistema junto con su nombre, etiqueta, ID de imagen, tamaño y fecha de creación.

**Ejemplo de salida:**

```bash
REPOSITORY          TAG       IMAGE ID       CREATED         SIZE
mynodeapp           1.0       0dfcf9dfd6d6   2 minutes ago   350MB
```

#### **Construcción de imágenes sin cache:**

Si quieres construir la imagen sin usar la caché de las capas anteriores (por ejemplo, si quieres asegurarte de que se ejecute todo desde cero), puedes usar la opción `--no-cache`:

```bash
docker build --no-cache -t mynodeapp:1.0 .
```

Este comando evita el uso de la caché de las capas y obliga a que Docker ejecute todas las instrucciones del `Dockerfile` de nuevo.

#### **Ver el registro de construcción:**

También puedes usar el `--progress` para obtener más detalles sobre el progreso de la construcción de la imagen.

```bash
docker build --progress=plain -t mynodeapp:1.0 .
```

Este comando te dará una salida más detallada sobre cómo Docker está construyendo la imagen y qué está ocurriendo en cada paso.

---

### **Resumen de los pasos para construir una imagen:**
1. **Crear un `Dockerfile` con los pasos necesarios**.
2. **Ejecutar `docker build -t <nombre>:<tag> .`** para construir la imagen.
3. **Usar `docker images` para verificar que la imagen fue construida correctamente**.
4. **(Opcional) Ejecutar `docker build --no-cache` para evitar usar la caché**.
