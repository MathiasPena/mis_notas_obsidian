
Docker proporciona una forma sencilla de gestionar redes, permitiendo que los contenedores se comuniquen entre sí de manera eficiente y segura. Las redes en Docker pueden ser usadas para conectar contenedores entre sí, aislar redes o definir configuraciones de seguridad.

#### **Listar las redes disponibles con `docker network ls`:**

Este comando muestra todas las redes disponibles en tu instalación de Docker. Las redes en Docker permiten que los contenedores se comuniquen entre sí, pero también pueden ser utilizadas para aislar contenedores de otras redes.

#### **Sintaxis:**
```bash
docker network ls
```

#### **Ejemplo:**
```bash
docker network ls
```

**Salida esperada:**
```bash
NETWORK ID          NAME                DRIVER              SCOPE
b1a6bbd1e407        bridge              bridge              local
c1e4edba3fd9        host                host                local
a3f9b8c5f7d7        none                null                local
```

En este caso:
- **bridge**: Es la red predeterminada para los contenedores, y se usa cuando no especificas otra red.
- **host**: Conexión directa con la red del host, eliminando la capa de virtualización.
- **none**: Sin red; es un contenedor sin conectividad de red.

#### **Crear una red con `docker network create`:**

Para crear una nueva red, puedes usar el comando `docker network create`. Esto te permite crear redes personalizadas que puedes usar para conectar contenedores. Existen diferentes tipos de redes, pero la más común es el tipo **bridge**.

#### **Sintaxis:**
```bash
docker network create <nombre_red>
```

#### **Ejemplo de creación de una red tipo bridge:**
```bash
docker network create my_network
```

Esto crea una red llamada `my_network`. Los contenedores que se conecten a esta red podrán comunicarse entre sí, pero estarán aislados de los contenedores que no pertenezcan a la misma red.

#### **Ver detalles de una red específica con `docker network inspect`:**

Para obtener más detalles sobre una red, puedes usar el comando `docker network inspect` seguido del nombre de la red.

```bash
docker network inspect my_network
```

**Salida esperada:**
```bash
[
    {
        "Name": "my_network",
        "Id": "f9a153fd84dfe10fb2b4d5598b8f1f2f6a78a02ccad6f01c",
        "Created": "2025-03-10T15:24:14.9472498Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
```

Esto proporciona detalles como:
- **Name**: El nombre de la red.
- **Id**: El identificador único de la red.
- **Driver**: El tipo de red (en este caso, `bridge`).
- **Subnet**: El rango de IPs utilizado por la red.
- **Gateway**: La puerta de enlace para la red.

#### **Eliminar una red con `docker network rm`:**

Si ya no necesitas una red, puedes eliminarla con el siguiente comando:

```bash
docker network rm my_network
```

Nota: Asegúrate de que no haya contenedores conectados a esa red antes de eliminarla. Si hay contenedores en uso, Docker te notificará y no se eliminará la red.

---

### **Resumen de los pasos para gestionar redes en Docker:**

1. **Listar las redes disponibles:**
   ```bash
   docker network ls
   ```

2. **Crear una red personalizada:**
   ```bash
   docker network create <nombre_red>
   ```

3. **Inspeccionar detalles de una red:**
   ```bash
   docker network inspect <nombre_red>
   ```

4. **Eliminar una red:**
   ```bash
   docker network rm <nombre_red>
   ```
