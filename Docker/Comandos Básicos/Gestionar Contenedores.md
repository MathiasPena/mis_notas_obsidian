
Una vez que los contenedores están en ejecución, es importante saber cómo administrarlos, ya sea para ver su estado, detenerlos o eliminarlos. Docker ofrece varios comandos para gestionar los contenedores y obtener información útil sobre ellos.

#### **Ver los contenedores en ejecución**

Para ver los contenedores que están actualmente en ejecución, utiliza el siguiente comando:

```bash
docker ps
```

Este comando mostrará una lista de los contenedores activos en el sistema, incluyendo detalles como su ID, nombre, puerto expuesto, tiempo de ejecución, y más.

**Ejemplo de salida:**

```bash
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
d5d2e0a1f2f7   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   80/tcp    mi_web
```

#### **Ver todos los contenedores (incluidos los detenidos)**

Si quieres ver todos los contenedores, incluyendo aquellos que no están en ejecución, usa la opción `-a` (all):

```bash
docker ps -a
```

Este comando también te mostrará los contenedores detenidos y su estado.

#### **Detener un contenedor en ejecución**

Para detener un contenedor que está en ejecución, usa el siguiente comando:

```bash
docker stop <container_id>
```

**Ejemplo:**

```bash
docker stop d5d2e0a1f2f7
```

El comando anterior detendrá el contenedor con ID `d5d2e0a1f2f7`.

#### **Detener múltiples contenedores**

Si deseas detener varios contenedores, puedes hacerlo pasando varios IDs o nombres de contenedor al comando `stop`.

**Ejemplo:**

```bash
docker stop contenedor1 contenedor2
```

Este comando detendrá tanto `contenedor1` como `contenedor2`.

#### **Eliminar un contenedor detenido**

Si un contenedor ya no es necesario y está detenido, puedes eliminarlo con el siguiente comando:

```bash
docker rm <container_id>
```

**Ejemplo:**

```bash
docker rm d5d2e0a1f2f7
```

Este comando eliminará el contenedor con ID `d5d2e0a1f2f7`. 

#### **Eliminar varios contenedores**

Para eliminar varios contenedores al mismo tiempo, puedes especificar varios IDs o nombres de contenedor.

**Ejemplo:**

```bash
docker rm contenedor1 contenedor2
```

#### **Detener y eliminar un contenedor en un solo comando**

Si quieres detener y eliminar un contenedor de manera inmediata, puedes encadenar ambos comandos o usar la opción `--rm` al ejecutar el contenedor.

**Detener y eliminar contenedor manualmente:**

```bash
docker stop d5d2e0a1f2f7 && docker rm d5d2e0a1f2f7
```

**O usando la opción `--rm`:**

```bash
docker run --rm nginx
```

En este caso, el contenedor `nginx` se eliminará automáticamente cuando se detenga.

#### **Reiniciar un contenedor**

Si necesitas reiniciar un contenedor en ejecución, puedes usar el comando `restart`:

```bash
docker restart <container_id>
```

**Ejemplo:**

```bash
docker restart d5d2e0a1f2f7
```

#### **Ver los logs de un contenedor**

Para ver los registros o logs de un contenedor, puedes usar el siguiente comando:

```bash
docker logs <container_id>
```

**Ejemplo:**

```bash
docker logs d5d2e0a1f2f7
```

Este comando te mostrará los logs del contenedor con el ID `d5d2e0a1f2f7`. Si el contenedor está ejecutando un servidor web, por ejemplo, verás los logs de acceso o errores.

#### **Seguir los logs en tiempo real**

Si deseas ver los logs en tiempo real, usa la opción `-f`:

```bash
docker logs -f <container_id>
```

**Ejemplo:**

```bash
docker logs -f d5d2e0a1f2f7
```

Esto te permitirá ver los nuevos registros que el contenedor genera mientras está en ejecución.

#### **Ver el uso de recursos de los contenedores**

Para obtener estadísticas en tiempo real sobre el uso de recursos (CPU, memoria, disco, red) de tus contenedores, puedes usar el comando `stats`:

```bash
docker stats
```

Este comando mostrará una lista de todos los contenedores activos y su uso de recursos en tiempo real.

#### **Ver la información detallada de un contenedor**

Si necesitas obtener información más detallada sobre un contenedor específico, puedes usar el comando `inspect`:

```bash
docker inspect <container_id>
```

**Ejemplo:**

```bash
docker inspect d5d2e0a1f2f7
```

Este comando devuelve información detallada en formato JSON, incluyendo configuraciones, volúmenes, redes y más.

#### **Limpiar contenedores detenidos**

Si tienes muchos contenedores detenidos que ya no necesitas, puedes eliminarlos todos con:

```bash
docker container prune
```

Esto eliminará todos los contenedores detenidos, liberando espacio en el sistema.

#### **Resumen de Comandos para Gestionar Contenedores:**

| Comando                    | Descripción                                               |
|----------------------------|-----------------------------------------------------------|
| `docker ps`                | Ver los contenedores en ejecución.                        |
| `docker ps -a`             | Ver todos los contenedores, incluidos los detenidos.      |
| `docker stop <id>`         | Detener un contenedor.                                   |
| `docker stop <id1> <id2>`  | Detener múltiples contenedores.                           |
| `docker rm <id>`           | Eliminar un contenedor detenido.                          |
| `docker rm <id1> <id2>`    | Eliminar múltiples contenedores detenidos.                |
| `docker restart <id>`      | Reiniciar un contenedor.                                  |
| `docker logs <id>`         | Ver los logs de un contenedor.                            |
| `docker logs -f <id>`      | Seguir los logs de un contenedor en tiempo real.          |
| `docker stats`             | Ver estadísticas de recursos de los contenedores.         |
| `docker inspect <id>`      | Ver información detallada de un contenedor.               |
| `docker container prune`   | Eliminar todos los contenedores detenidos.                |

Con estos comandos puedes gestionar contenedores de manera efectiva y realizar tareas comunes como ver su estado, detenerlos, eliminarlos y obtener detalles de su ejecución.

