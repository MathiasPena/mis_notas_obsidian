
Las operaciones básicas en SQL son fundamentales para interactuar con los datos almacenados en una base de datos. Estas operaciones permiten consultar, insertar, actualizar y eliminar datos. Vamos a ver cómo funcionan las principales operaciones: **SELECT**, **FROM**, y **WHERE**.

## SELECT

La operación **SELECT** se utiliza para recuperar datos de una base de datos. Es la consulta más común en SQL, y permite seleccionar una o más columnas de una o varias tablas.

### Sintaxis Básica:

```sql
SELECT columna1, columna2, ...
FROM tabla;
```

### Ejemplo:

```sql
SELECT nombre, email
FROM Clientes;
```

Este ejemplo devuelve las columnas `nombre` y `email` de todos los registros en la tabla `Clientes`.

### Seleccionar todas las columnas:

Si deseas seleccionar todas las columnas de una tabla, puedes usar el asterisco `*`.

```sql
SELECT *
FROM Clientes;
```

Esto devuelve todos los registros de la tabla `Clientes`, incluyendo todas sus columnas.

## FROM

La operación **FROM** especifica la tabla o tablas de donde se van a seleccionar los datos. Se utiliza junto con **SELECT** para indicar la fuente de los datos.

### Ejemplo:

```sql
SELECT *
FROM Pedidos;
```

Este ejemplo selecciona todos los datos de la tabla `Pedidos`.

### Joins (Operaciones con varias tablas)

Puedes combinar varias tablas utilizando el operador `JOIN`. Por ejemplo, para combinar las tablas `Clientes` y `Pedidos`:

```sql
SELECT Clientes.nombre, Pedidos.id_pedido
FROM Clientes
JOIN Pedidos ON Clientes.id_cliente = Pedidos.id_cliente;
```

Este ejemplo recupera el nombre de los clientes y los IDs de los pedidos correspondientes.

## WHERE

La cláusula **WHERE** se utiliza para filtrar los resultados de una consulta, aplicando condiciones específicas. Permite seleccionar solo aquellos registros que cumplan con una condición dada.

### Sintaxis Básica:

```sql
SELECT columna1, columna2, ...
FROM tabla
WHERE condición;
```

### Ejemplo:

```sql
SELECT nombre, email
FROM Clientes
WHERE id_cliente = 1;
```

Este ejemplo selecciona el nombre y el email del cliente con `id_cliente` igual a 1.

### Operadores comunes en WHERE:

- **=**: Igual.
- **<>** o **!=**: Diferente.
- **>**: Mayor que.
- **<**: Menor que.
- **>=**: Mayor o igual que.
- **<=**: Menor o igual que.
- **BETWEEN**: Rango de valores.
- **LIKE**: Coincidencia de patrones.
- **IN**: Coincidencia en una lista de valores.

#### Ejemplo con operador `BETWEEN`:

```sql
SELECT nombre, email
FROM Clientes
WHERE id_cliente BETWEEN 1 AND 3;
```

Este ejemplo selecciona a los clientes cuyo `id_cliente` está entre 1 y 3, inclusivo.

#### Ejemplo con operador `LIKE`:

```sql
SELECT nombre, email
FROM Clientes
WHERE nombre LIKE 'Juan%';
```

Este ejemplo selecciona todos los clientes cuyo nombre comienza con "Juan".

#### Ejemplo con operador `IN`:

```sql
SELECT nombre, email
FROM Clientes
WHERE id_cliente IN (1, 3, 5);
```

Este ejemplo selecciona los clientes con `id_cliente` igual a 1, 3 o 5.

## Resumen de SELECT, FROM, WHERE

- **SELECT**: Recupera los datos de las columnas que especifiques.
- **FROM**: Especifica las tablas de donde se van a recuperar los datos.
- **WHERE**: Filtra los datos según una condición.