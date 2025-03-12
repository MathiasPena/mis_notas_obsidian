
Una vez que has creado un volumen, puedes montarlo dentro de un contenedor para persistir datos generados por ese contenedor. Esto asegura que incluso si el contenedor se elimina, los datos no se perderán, ya que permanecerán almacenados en el volumen.

#### **Sintaxis:**
```bash
docker run -v <host_path>:<container_path> <imagen>
```
- **`<host_path>`**: Es la ruta en tu máquina host (el sistema operativo en el que corre Docker) donde se almacenarán los datos.
- **`<container_path>`**: Es la ruta dentro del contenedor donde los datos se montarán.
- **`<imagen>`**: Es la imagen de Docker que se usará para crear el contenedor.

#### **Montar un volumen creado previamente:**

Si ya tienes un volumen creado (por ejemplo, `my_volume`), puedes montarlo dentro del contenedor usando el siguiente comando:

```bash
docker run -v my_volume:/data myapp:latest
```

Este comando hará lo siguiente:
- Ejecutará un contenedor a partir de la imagen `myapp:latest`.
- Montará el volumen `my_volume` en la ruta `/data` dentro del contenedor.
- Cualquier archivo creado o modificado en `/data` dentro del contenedor se almacenará en el volumen, lo que asegura que los cambios persistan incluso si el contenedor se elimina.

#### **Ejemplo con ruta del sistema de archivos del host:**

Si prefieres usar una ruta específica del sistema de archivos del host en lugar de un volumen, puedes especificar directamente una ruta de tu máquina local.

```bash
docker run -v /home/user/data:/data myapp:latest
```

En este caso:
- La carpeta `/home/user/data` en tu máquina local se monta como `/data` dentro del contenedor.
- Cualquier cambio en los archivos dentro del contenedor en `/data` se reflejará en la carpeta `/home/user/data` en el host.

#### **Montar múltiples volúmenes:**

Puedes montar varios volúmenes en un contenedor si es necesario, separándolos con más de una opción `-v`.

```bash
docker run -v my_volume:/data -v /home/user/config:/config myapp:latest
```

Este comando montará dos volúmenes:
- `my_volume` en `/data` dentro del contenedor.
- La carpeta `/home/user/config` del host en `/config` dentro del contenedor.

#### **Montar volúmenes de solo lectura:**

Si quieres montar un volumen como solo lectura (es decir, los contenedores solo pueden leer los datos y no modificarlos), puedes usar la opción `:ro` al final de la ruta del contenedor.

```bash
docker run -v my_volume:/data:ro myapp:latest
```

Con esto, los datos en `/data` dentro del contenedor solo serán accesibles para lectura y no podrán ser modificados.

#### **Montar un volumen anónimo:**

Si no quieres crear un volumen explícitamente, Docker puede crear un volumen anónimo por ti si solo usas la ruta del contenedor:

```bash
docker run -v /data myapp:latest
```

En este caso, Docker creará un volumen anónimo para `/data` dentro del contenedor y almacenará los datos en él.

#### **Ver los volúmenes montados en un contenedor:**

Para ver los volúmenes montados en un contenedor que está en ejecución, puedes usar el comando `docker inspect`:

```bash
docker inspect <container_id>
```

Este comando te dará información detallada sobre el contenedor, incluidos los volúmenes montados y sus rutas correspondientes.

#### **Eliminar un contenedor con volúmenes montados:**

Si deseas eliminar un contenedor pero mantener los volúmenes, puedes hacerlo sin problemas. Los volúmenes no se eliminan automáticamente al detener o eliminar un contenedor (a menos que uses la opción `--volumes` al eliminar).

```bash
docker rm <container_id>
```

Esto eliminará el contenedor pero mantendrá los volúmenes.

---

### **Resumen de los pasos para montar volúmenes:**

1. **Montar un volumen preexistente en el contenedor:**
   ```bash
   docker run -v my_volume:/data myapp:latest
   ```

2. **Montar una carpeta del host en el contenedor:**
   ```bash
   docker run -v /host/path:/container/path myapp:latest
   ```

3. **Montar múltiples volúmenes:**
   ```bash
   docker run -v volume1:/data -v /host/path:/config myapp:latest
   ```

4. **Montar un volumen de solo lectura:**
   ```bash
   docker run -v my_volume:/data:ro myapp:latest
   ```

5. **Ver los volúmenes montados en un contenedor:**
   ```bash
   docker inspect <container_id>
   ```
