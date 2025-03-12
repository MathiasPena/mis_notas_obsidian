
En una base de datos relacional, los datos se organizan en **tablas**. Cada tabla tiene filas y columnas, y cada fila contiene un conjunto de datos, mientras que las columnas representan los diferentes atributos de esos datos.

## Tablas

Una **tabla** es una colección de datos organizados en filas y columnas. Cada tabla tiene un nombre único dentro de la base de datos y está diseñada para almacenar información sobre un tipo específico de entidad.

### Ejemplo de tabla de Clientes:

```plaintext
Clientes
| id_cliente | nombre     | email           |
|------------|------------|-----------------|
| 1          | Juan Pérez | juan@email.com   |
| 2          | Ana Gómez  | ana@email.com    |
```

En este caso, la tabla `Clientes` tiene 3 columnas: `id_cliente`, `nombre`, y `email`, y 2 filas con los datos correspondientes a dos clientes.

## Filas

Una **fila** (o registro) es una colección de datos que representa una instancia única de una entidad en la tabla. Cada fila contiene valores para cada una de las columnas.

### Ejemplo de fila en la tabla de `Clientes`:

```plaintext
| id_cliente | nombre     | email           |
|------------|------------|-----------------|
| 1          | Juan Pérez | juan@email.com   |
```

En este caso, la fila representa a un cliente con un `id_cliente` de 1, `nombre` "Juan Pérez" y `email` "juan@email.com".

## Columnas

Una **columna** define un tipo de dato para una propiedad o atributo específico de las filas en una tabla. Cada columna tiene un nombre único dentro de la tabla y almacena un tipo de dato específico, como texto, números o fechas.

### Ejemplo de columna en la tabla de `Clientes`:

```plaintext
| id_cliente | nombre     | email           |
|------------|------------|-----------------|
| 1          | Juan Pérez | juan@email.com   |
| 2          | Ana Gómez  | ana@email.com    |
```

Las columnas `id_cliente`, `nombre`, y `email` representan las propiedades de cada cliente.

## Relación entre Filas y Columnas

Cada **fila** debe contener un valor para cada **columna**. El conjunto de valores de una fila debe respetar el tipo de datos definido en cada columna. Por ejemplo:

- En la columna `id_cliente`, el tipo de dato puede ser `INT` (entero), y cada fila debe tener un número único en esta columna.
- En la columna `email`, el tipo de dato puede ser `VARCHAR(100)`, y cada fila debe contener una cadena de texto con una dirección de correo electrónico.

## Ejemplo Completo de una Tabla de Pedidos

```plaintext
Pedidos
| id_pedido | id_cliente | id_producto | cantidad |
|-----------|------------|-------------|----------|
| 1         | 1          | 101         | 2        |
| 2         | 2          | 102         | 1        |
```

En la tabla `Pedidos`, cada fila representa un pedido realizado por un cliente. Las columnas `id_pedido`, `id_cliente`, `id_producto` y `cantidad` son necesarias para describir completamente un pedido.

## Crear una Tabla en SQL

El SQL para crear una tabla con filas y columnas es bastante sencillo. Aquí tienes un ejemplo para crear una tabla de clientes:

```sql
CREATE TABLE Clientes (
    id_cliente INT PRIMARY KEY,
    nombre VARCHAR(100),
    email VARCHAR(100)
);
```

En este ejemplo, hemos creado una tabla llamada `Clientes`, con tres columnas: `id_cliente`, `nombre`, y `email`. La columna `id_cliente` es la clave primaria de la tabla, lo que garantiza que cada cliente tendrá un identificador único.

## Resumen

Las **tablas** son la estructura principal en una base de datos relacional, y están compuestas por **filas** (registros) y **columnas** (atributos). Las filas contienen los datos individuales de cada entidad, mientras que las columnas definen qué tipo de datos se almacenan. Las relaciones entre tablas se hacen mediante claves primarias y foráneas, lo que asegura la integridad de los datos.
