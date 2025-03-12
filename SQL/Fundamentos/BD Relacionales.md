
Las bases de datos relacionales son un tipo de sistema de gestión de bases de datos (DBMS) que organiza los datos en tablas que están relacionadas entre sí. Estas bases de datos se basan en el modelo relacional propuesto por Edgar F. Codd en 1970, donde los datos son representados en forma de relaciones (tablas) y se pueden realizar consultas usando SQL.

## Características Clave de las Bases de Datos Relacionales

1. **Tablas**: Son las estructuras básicas de almacenamiento. Cada tabla está formada por filas y columnas.
2. **Filas**: Cada fila en una tabla representa un registro individual.
3. **Columnas**: Las columnas representan los atributos o campos del registro.

### Ventajas:
- **Integridad de los datos**: El modelo asegura que los datos se almacenan de forma organizada, reduciendo la redundancia.
- **Relaciones entre tablas**: Las tablas pueden estar relacionadas entre sí mediante claves primarias y foráneas.

## Ejemplo de Base de Datos Relacional

Consideremos una base de datos para una tienda online. Podría tener las siguientes tablas:

- **Clientes**
- **Productos**
- **Pedidos**

Cada una de estas tablas tendría diferentes columnas y relaciones entre ellas.

```plaintext
Clientes
| id_cliente | nombre     | email           |
|------------|------------|-----------------|
| 1          | Juan Pérez | juan@email.com   |
| 2          | Ana Gómez  | ana@email.com    |

Productos
| id_producto | nombre     | precio |
|-------------|------------|--------|
| 101         | Camiseta   | 20.00  |
| 102         | Pantalón   | 40.00  |

Pedidos
| id_pedido | id_cliente | id_producto | cantidad |
|-----------|------------|-------------|----------|
| 1         | 1          | 101         | 2        |
| 2         | 2          | 102         | 1        |
```

En este ejemplo, las tablas `Clientes`, `Productos` y `Pedidos` están relacionadas entre sí por las claves primarias y foráneas.

## Relacionando Tablas

- **Clave Primaria**: Es un campo (o conjunto de campos) que identifica de manera única cada registro en una tabla. Ejemplo: `id_cliente` en la tabla `Clientes`.
- **Clave Foránea**: Es un campo en una tabla que se refiere a la clave primaria en otra tabla. En el ejemplo anterior, `id_cliente` en la tabla `Pedidos` es una clave foránea que hace referencia a `id_cliente` en la tabla `Clientes`.

### Ejemplo de Relación:

Un cliente puede tener múltiples pedidos, pero cada pedido está asociado con un solo cliente. Esto es un ejemplo de **relación uno a muchos**.

```sql
-- Crear tabla Clientes
CREATE TABLE Clientes (
    id_cliente INT PRIMARY KEY,
    nombre VARCHAR(100),
    email VARCHAR(100)
);

-- Crear tabla Productos
CREATE TABLE Productos (
    id_producto INT PRIMARY KEY,
    nombre VARCHAR(100),
    precio DECIMAL(10, 2)
);

-- Crear tabla Pedidos
CREATE TABLE Pedidos (
    id_pedido INT PRIMARY KEY,
    id_cliente INT,
    id_producto INT,
    cantidad INT,
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente),
    FOREIGN KEY (id_producto) REFERENCES Productos(id_producto)
);
```

## Resumen

Las bases de datos relacionales utilizan tablas para organizar la información. Las tablas están relacionadas entre sí mediante claves primarias y foráneas. Este modelo permite garantizar la integridad de los datos y establecer relaciones entre diferentes entidades de forma eficiente.
