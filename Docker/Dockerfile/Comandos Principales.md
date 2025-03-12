
Los comandos dentro de un `Dockerfile` definen cómo se construye la imagen personalizada. A continuación se detallan los comandos principales que se utilizan para configurar y personalizar una imagen:

#### **FROM**

El comando `FROM` es obligatorio en cualquier `Dockerfile`, ya que especifica la imagen base desde la cual se va a construir la nueva imagen. Es la primera línea del archivo y debe estar seguida por una imagen existente.

**Sintaxis:**
```dockerfile
FROM <imagen_base>
```

**Ejemplo:**
```dockerfile
FROM ubuntu:20.04
```

#### **RUN**

El comando `RUN` se usa para ejecutar comandos dentro del contenedor durante el proceso de construcción de la imagen. Esto es útil para instalar dependencias o realizar configuraciones necesarias.

**Sintaxis:**
```dockerfile
RUN <comando>
```

**Ejemplo:**
```dockerfile
RUN apt-get update && apt-get install -y python3
```

Este comando ejecutará `apt-get update` y luego instalará Python3 dentro de la imagen.

#### **COPY**

El comando `COPY` se utiliza para copiar archivos desde el sistema local hacia la imagen. Puedes especificar tanto archivos como directorios completos.

**Sintaxis:**
```dockerfile
COPY <origen> <destino>
```

**Ejemplo:**
```dockerfile
COPY ./app /usr/src/app
```

Este comando copia todos los archivos del directorio `./app` en tu máquina local a `/usr/src/app` dentro del contenedor.

#### **WORKDIR**

El comando `WORKDIR` establece el directorio de trabajo dentro del contenedor. Las instrucciones `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, y `ADD` se ejecutarán desde este directorio.

**Sintaxis:**
```dockerfile
WORKDIR <ruta_directorio>
```

**Ejemplo:**
```dockerfile
WORKDIR /app
```

Este comando establece `/app` como el directorio de trabajo en el contenedor.

#### **CMD**

El comando `CMD` especifica el comando por defecto que se ejecutará cuando se inicie el contenedor. Puede aceptar varias formas de escritura: 

- **Forma exec** (recomendada) para especificar un comando y sus argumentos como una lista JSON.
- **Forma Shell** para escribir un comando como una cadena de texto (menos recomendable).

**Sintaxis:**
```dockerfile
CMD ["comando", "argumento1", "argumento2"]
```
o
```dockerfile
CMD ["comando"]
```

**Ejemplo:**
```dockerfile
CMD ["python", "app.py"]
```

Este comando ejecutará `python app.py` cuando se inicie el contenedor.

#### **EXPOSE**

El comando `EXPOSE` informa a Docker que el contenedor escuchará en los puertos especificados en tiempo de ejecución. Esto no abre los puertos, pero actúa como una señal de que el contenedor usará estos puertos.

**Sintaxis:**
```dockerfile
EXPOSE <puerto>
```

**Ejemplo:**
```dockerfile
EXPOSE 80
```

Este comando indica que el contenedor escuchará en el puerto 80.

#### **ENTRYPOINT**

El comando `ENTRYPOINT` define el comando que se ejecutará de manera predeterminada cuando se inicie el contenedor. A diferencia de `CMD`, `ENTRYPOINT` no se puede reemplazar fácilmente cuando se inicia el contenedor, a menos que uses la opción `--entrypoint` al ejecutar `docker run`.

**Sintaxis:**
```dockerfile
ENTRYPOINT ["comando", "argumento1", "argumento2"]
```

**Ejemplo:**
```dockerfile
ENTRYPOINT ["python", "app.py"]
```

Este comando garantiza que `python app.py` siempre se ejecute al iniciar el contenedor.

#### **ADD**

El comando `ADD` tiene una funcionalidad similar a `COPY`, pero con más capacidades. `ADD` puede manejar URLs remotas y archivos comprimidos (tarballs), los cuales se descomprimirán automáticamente al ser añadidos al contenedor.

**Sintaxis:**
```dockerfile
ADD <origen> <destino>
```

**Ejemplo:**
```dockerfile
ADD ./myapp.tar.gz /usr/src/app
```

Este comando extrae el archivo comprimido `myapp.tar.gz` y lo descomprime en el directorio `/usr/src/app`.

#### **VOLUME**

El comando `VOLUME` se utiliza para crear un punto de montaje dentro del contenedor, que puede ser utilizado para almacenar datos persistentes que se mantienen incluso después de que el contenedor sea detenido o eliminado.

**Sintaxis:**
```dockerfile
VOLUME ["/path/to/volume"]
```

**Ejemplo:**
```dockerfile
VOLUME ["/data"]
```

Este comando crea un volumen en el directorio `/data` dentro del contenedor.

---

### Resumen de comandos principales:

| Comando       | Descripción |
|---------------|-------------|
| `FROM`        | Especifica la imagen base desde la cual se construye la nueva imagen. |
| `RUN`         | Ejecuta comandos dentro del contenedor durante la construcción de la imagen. |
| `COPY`        | Copia archivos desde el sistema local al contenedor. |
| `WORKDIR`     | Establece el directorio de trabajo dentro del contenedor. |
| `CMD`         | Especifica el comando que se ejecutará cuando se inicie el contenedor. |
| `EXPOSE`      | Expone los puertos para que el contenedor pueda ser accedido externamente. |
| `ENTRYPOINT`  | Define el comando que se ejecutará siempre cuando se inicie el contenedor. |
| `ADD`         | Similar a `COPY`, pero con más funcionalidades (maneja URLs y archivos comprimidos). |
| `VOLUME`      | Crea un punto de montaje en el contenedor para almacenar datos persistentes. |
