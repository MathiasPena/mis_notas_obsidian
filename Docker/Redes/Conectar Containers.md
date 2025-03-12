
Una de las principales ventajas de las redes en Docker es la capacidad de conectar contenedores entre sí. Esto permite que los contenedores se comuniquen de forma aislada, pero efectiva. Usar redes específicas para conectar contenedores puede mejorar la seguridad y la organización de tu infraestructura de contenedores.

#### **Sintaxis:**
Cuando creas un contenedor, puedes conectarlo a una red utilizando la opción `--network`:

```bash
docker run --network <nombre_red> <imagen>
```

#### **Ejemplo de conexión de un contenedor a una red:**
Imagina que tienes una red llamada `my_network` y quieres ejecutar un contenedor en esa red:

```bash
docker run -d --name my_container --network my_network nginx
```

Este comando ejecutará el contenedor `nginx` y lo conectará a la red `my_network`.

#### **Ver contenedores conectados a una red:**

Si quieres ver qué contenedores están conectados a una red específica, puedes inspeccionar la red con el siguiente comando:

```bash
docker network inspect my_network
```

Esto te dará información detallada sobre los contenedores conectados a esa red.

**Salida esperada:**
```bash
[
    {
        "Name": "my_network",
        "Id": "f9a153fd84dfe10fb2b4d5598b8f1f2f6a78a02ccad6f01c",
        "Containers": {
            "cdbed4d1f0c2": {
                "Name": "my_container",
                "EndpointID": "f8f9a74245db6b2e8d4d9fd1e928a50204a3e9e4b9cc7b88bb",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
```

En este caso, podemos ver que el contenedor `my_container` está conectado a la red `my_network`, y se le ha asignado una dirección IP interna (`172.18.0.2`).

#### **Conectar un contenedor a una red existente:**

Si un contenedor ya está en ejecución y deseas conectarlo a una red existente, puedes usar el comando `docker network connect`:

```bash
docker network connect my_network my_container
```

Esto conectará al contenedor `my_container` a la red `my_network` sin detenerlo.

#### **Desconectar un contenedor de una red:**

Si deseas desconectar un contenedor de una red, usa el comando `docker network disconnect`:

```bash
docker network disconnect my_network my_container
```

Este comando desconectará el contenedor `my_container` de la red `my_network`, lo que podría afectar las comunicaciones si otros contenedores dependen de él.

#### **Conexión entre contenedores a través de nombres de red:**

Uno de los beneficios de usar redes en Docker es que los contenedores pueden comunicarse entre sí usando sus nombres de contenedor como DNS. Esto significa que un contenedor puede acceder a otro contenedor usando el nombre de su contenedor en lugar de una dirección IP.

Por ejemplo, si tienes dos contenedores conectados a la misma red (`my_network`), puedes hacer que un contenedor `container1` se conecte a `container2` usando el nombre `container2`:

```bash
docker run --network my_network --name container1 -d nginx
docker run --network my_network --name container2 -d nginx
```

Dentro de `container1`, podrías hacer una solicitud a `container2` por su nombre:

```bash
curl http://container2
```

Docker se encargará de la resolución del nombre y hará que `container1` se conecte a `container2` sin que necesites especificar una IP.

---

### **Resumen de los pasos para conectar contenedores:**

1. **Crear y ejecutar un contenedor en una red específica:**
   ```bash
   docker run -d --name my_container --network my_network nginx
   ```

2. **Ver contenedores conectados a una red:**
   ```bash
   docker network inspect my_network
   ```

3. **Conectar un contenedor en ejecución a una red:**
   ```bash
   docker network connect my_network my_container
   ```

4. **Desconectar un contenedor de una red:**
   ```bash
   docker network disconnect my_network my_container
   ```

5. **Comunicación entre contenedores usando nombres de contenedor:**
   ```bash
   curl http://container2
   ```
