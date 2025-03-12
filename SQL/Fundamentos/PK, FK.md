
Las **claves primarias** y **claves foráneas** son esenciales para mantener la integridad y las relaciones entre las tablas en una base de datos relacional. Estas claves permiten identificar registros de manera única y conectar diferentes tablas entre sí.

## Clave Primaria

Una **clave primaria** (Primary Key) es un campo o un conjunto de campos en una tabla que **identifica de manera única** cada registro dentro de esa tabla. No puede haber dos registros con el mismo valor en la clave primaria.

### Características de la Clave Primaria:

- Debe ser única: cada valor en la columna debe ser distinto.
- No puede ser nula: siempre debe tener un valor.
- Puede ser una columna o varias (combinada).

### Ejemplo de Clave Primaria:

En la siguiente tabla, `id_cliente` es la clave primaria de la tabla `Clientes`, lo que asegura que cada cliente tenga un identificador único.

```plaintext
Clientes
| id_cliente (PK) | nombre     | email           |
|-----------------|------------|-----------------|
| 1               | Juan Pérez | juan@email.com   |
| 2               | Ana Gómez  | ana@email.com    |
```

En este caso, **`id_cliente`** es único para cada fila y se utiliza para identificar de manera única a cada cliente.

### SQL para Definir una Clave Primaria:

```sql
CREATE TABLE Clientes (
    id_cliente INT PRIMARY KEY,
    nombre VARCHAR(100),
    email VARCHAR(100)
);
```

## Clave Foránea

Una **clave foránea** (Foreign Key) es un campo o un conjunto de campos en una tabla que **se refiere a la clave primaria** de otra tabla. Las claves foráneas se utilizan para establecer y reforzar los vínculos entre las tablas.

### Características de la Clave Foránea:

- Puede tener valores duplicados: es posible que varios registros en la tabla referencien el mismo valor en la clave primaria.
- Puede ser nula: si no hay una relación, se puede dejar vacía.
- Establece relaciones de **uno a muchos** o **muchos a muchos** entre las tablas.

### Ejemplo de Clave Foránea:

En la tabla `Pedidos`, la columna `id_cliente` es una clave foránea que se refiere a la clave primaria `id_cliente` en la tabla `Clientes`. Esto indica que cada pedido está asociado a un cliente.

```plaintext
Pedidos
| id_pedido | id_cliente (FK) | id_producto | cantidad |
|-----------|-----------------|-------------|----------|
| 1         | 1               | 101         | 2        |
| 2         | 2               | 102         | 1        |
```

En este caso, **`id_cliente`** en la tabla `Pedidos` se refiere a **`id_cliente`** en la tabla `Clientes`, creando una relación entre las dos tablas.

### SQL para Definir una Clave Foránea:

```sql
CREATE TABLE Pedidos (
    id_pedido INT PRIMARY KEY,
    id_cliente INT,
    id_producto INT,
    cantidad INT,
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente)
);
```

En este ejemplo, **`id_cliente`** en la tabla `Pedidos` es una clave foránea que hace referencia a **`id_cliente`** en la tabla `Clientes`.

## Relación entre Clave Primaria y Clave Foránea

Las claves foráneas permiten que una tabla "apunte" a otra, creando relaciones entre las tablas. En nuestro ejemplo:

- Un cliente puede tener múltiples pedidos (relación **uno a muchos**).
- Un pedido está asociado a un solo cliente, pero puede contener varios productos.

Esto permite gestionar las relaciones entre diferentes entidades de forma estructurada y asegura la integridad referencial, es decir, garantiza que los valores en la clave foránea existan como claves primarias en la otra tabla.

### Ejemplo Visual:

```plaintext
Clientes                        Pedidos
| id_cliente (PK) | nombre     | id_cliente (FK) | id_pedido |
|-----------------|------------|-----------------|-----------|
| 1               | Juan Pérez | 1               | 1         |
| 2               | Ana Gómez  | 2               | 2         |

```

## Resumen

- **Clave Primaria**: Identifica de manera única un registro dentro de una tabla.
- **Clave Foránea**: Establece una relación entre dos tablas, apuntando a una clave primaria de otra tabla.
- Estas claves son fundamentales para mantener la integridad y las relaciones entre los datos en una base de datos relacional.
