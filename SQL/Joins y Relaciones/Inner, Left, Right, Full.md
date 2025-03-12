
### 1. **INNER JOIN**

El **INNER JOIN** es el tipo de join más común. Devuelve solo las filas que tienen coincidencias en ambas tablas involucradas en el join.

#### Ejemplos:

- **Unir dos tablas por una columna común:**

```sql
SELECT Empleados.nombre, Departamentos.nombre
FROM Empleados
INNER JOIN Departamentos
ON Empleados.departamento_id = Departamentos.id;
```
Este ejemplo muestra los nombres de los empleados y sus respectivos departamentos, solo para los empleados que están asignados a un departamento.

- **INNER JOIN con varias condiciones:**

```sql
SELECT Clientes.nombre, Pedidos.id_pedido, Pedidos.fecha
FROM Clientes
INNER JOIN Pedidos
ON Clientes.id_cliente = Pedidos.id_cliente
AND Pedidos.estado = 'Enviado';
```
Este ejemplo selecciona los clientes y sus pedidos que han sido enviados.

- **INNER JOIN entre tres tablas:**

```sql
SELECT Empleados.nombre, Departamentos.nombre, Proyectos.nombre
FROM Empleados
INNER JOIN Departamentos ON Empleados.departamento_id = Departamentos.id
INNER JOIN Proyectos ON Empleados.proyecto_id = Proyectos.id;
```
Este ejemplo obtiene los nombres de empleados, departamentos y proyectos relacionados entre sí.

---

### 2. **LEFT JOIN (o LEFT OUTER JOIN)**

El **LEFT JOIN** devuelve todas las filas de la tabla de la izquierda (primera tabla), y las filas coincidentes de la tabla de la derecha (segunda tabla). Si no hay coincidencias, el resultado de la tabla de la derecha será `NULL`.

#### Ejemplos:

- **Unir una tabla con todas sus filas y las coincidentes de la otra:**

```sql
SELECT Clientes.nombre, Pedidos.id_pedido
FROM Clientes
LEFT JOIN Pedidos
ON Clientes.id_cliente = Pedidos.id_cliente;
```
Este ejemplo devuelve todos los clientes, y solo los pedidos que coincidan con ellos. Si un cliente no tiene pedidos, se mostrará `NULL` en la columna de `id_pedido`.

- **LEFT JOIN con una condición:**

```sql
SELECT Empleados.nombre, Proyectos.nombre
FROM Empleados
LEFT JOIN Proyectos
ON Empleados.proyecto_id = Proyectos.id
WHERE Proyectos.nombre IS NULL;
```
Este ejemplo selecciona a los empleados que no están asignados a ningún proyecto.

---

### 3. **RIGHT JOIN (o RIGHT OUTER JOIN)**

El **RIGHT JOIN** es lo contrario del **LEFT JOIN**. Devuelve todas las filas de la tabla de la derecha (segunda tabla) y las filas coincidentes de la tabla de la izquierda (primera tabla). Si no hay coincidencias, el resultado de la tabla de la izquierda será `NULL`.

#### Ejemplos:

- **RIGHT JOIN básico:**

```sql
SELECT Pedidos.id_pedido, Clientes.nombre
FROM Pedidos
RIGHT JOIN Clientes
ON Pedidos.id_cliente = Clientes.id_cliente;
```
Este ejemplo devuelve todos los clientes y sus pedidos. Si un cliente no tiene pedido, la columna `id_pedido` será `NULL`.

- **RIGHT JOIN con condición:**

```sql
SELECT Productos.nombre, Proveedores.nombre
FROM Productos
RIGHT JOIN Proveedores
ON Productos.proveedor_id = Proveedores.id;
```
Este ejemplo selecciona todos los proveedores y sus productos, mostrando `NULL` en la columna de productos cuando no haya coincidencia.

---

### 4. **FULL JOIN (o FULL OUTER JOIN)**

El **FULL JOIN** devuelve todas las filas cuando hay una coincidencia en cualquiera de las tablas. Si no hay coincidencia, se devolverá `NULL` en la tabla sin coincidencia.

#### Ejemplos:

- **FULL JOIN básico:**

```sql
SELECT Empleados.nombre, Proyectos.nombre
FROM Empleados
FULL JOIN Proyectos
ON Empleados.proyecto_id = Proyectos.id;
```
Este ejemplo devuelve todos los empleados y todos los proyectos. Si un empleado no está asignado a un proyecto, o si un proyecto no tiene empleados asignados, se mostrará `NULL` en las columnas correspondientes.

- **FULL JOIN con varias tablas:**

```sql
SELECT Clientes.nombre, Pedidos.id_pedido, Productos.nombre
FROM Clientes
FULL JOIN Pedidos ON Clientes.id_cliente = Pedidos.id_cliente
FULL JOIN Productos ON Pedidos.id_pedido = Productos.id_pedido;
```
Este ejemplo devuelve todos los clientes, pedidos y productos, mostrando `NULL` cuando no hay coincidencias.

---

### Resumen

- **INNER JOIN**: Devuelve solo las filas con coincidencias en ambas tablas.
- **LEFT JOIN**: Devuelve todas las filas de la tabla de la izquierda y las coincidencias de la tabla de la derecha (con `NULL` donde no hay coincidencia).
- **RIGHT JOIN**: Devuelve todas las filas de la tabla de la derecha y las coincidencias de la tabla de la izquierda (con `NULL` donde no hay coincidencia).
- **FULL JOIN**: Devuelve todas las filas cuando hay una coincidencia en cualquiera de las tablas, con `NULL` donde no hay coincidencia.
