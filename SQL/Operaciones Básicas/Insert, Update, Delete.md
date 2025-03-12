
Estas operaciones permiten modificar los datos dentro de las tablas de una base de datos. Son esenciales para manejar la información de manera dinámica: **INSERT** agrega nuevos registros, **UPDATE** modifica registros existentes, y **DELETE** elimina registros.

## INSERT

La operación **INSERT** se utiliza para agregar nuevos registros a una tabla.

### Sintaxis Básica:

```sql
INSERT INTO tabla (columna1, columna2, ...)
VALUES (valor1, valor2, ...);
```

### Ejemplo:

```sql
INSERT INTO Clientes (id_cliente, nombre, email)
VALUES (3, 'Carlos Rodríguez', 'carlos@email.com');
```

Este ejemplo inserta un nuevo cliente con `id_cliente` igual a 3, `nombre` "Carlos Rodríguez" y `email` "carlos@email.com" en la tabla `Clientes`.

### Insertar múltiples registros:

También puedes insertar varios registros a la vez.

```sql
INSERT INTO Clientes (id_cliente, nombre, email)
VALUES 
(4, 'Laura Sánchez', 'laura@email.com'),
(5, 'Pedro Díaz', 'pedro@email.com');
```

Este ejemplo agrega dos nuevos clientes a la tabla `Clientes`.

## UPDATE

La operación **UPDATE** se utiliza para modificar registros existentes en una tabla. Es importante usar **WHERE** para asegurarse de que solo se actualicen los registros correctos.

### Sintaxis Básica:

```sql
UPDATE tabla
SET columna1 = valor1, columna2 = valor2, ...
WHERE condición;
```

### Ejemplo:

```sql
UPDATE Clientes
SET email = 'nuevoemail@email.com'
WHERE id_cliente = 1;
```

Este ejemplo actualiza el correo electrónico del cliente con `id_cliente` igual a 1.

### Actualizar múltiples columnas:

También puedes actualizar varias columnas al mismo tiempo.

```sql
UPDATE Clientes
SET nombre = 'Juan López', email = 'juanlopez@email.com'
WHERE id_cliente = 1;
```

Este ejemplo actualiza tanto el `nombre` como el `email` del cliente con `id_cliente` igual a 1.

## DELETE

La operación **DELETE** se utiliza para eliminar registros de una tabla. Al igual que con **UPDATE**, es crucial usar **WHERE** para evitar eliminar registros accidentalmente.

### Sintaxis Básica:

```sql
DELETE FROM tabla
WHERE condición;
```

### Ejemplo:

```sql
DELETE FROM Clientes
WHERE id_cliente = 3;
```

Este ejemplo elimina el cliente con `id_cliente` igual a 3 de la tabla `Clientes`.

### Eliminar todos los registros:

Si omites la cláusula **WHERE**, eliminarás todos los registros de la tabla.

```sql
DELETE FROM Clientes;
```

Este comando elimina todos los registros en la tabla `Clientes`, pero la estructura de la tabla permanece intacta.

## Resumen de INSERT, UPDATE, DELETE

- **INSERT**: Se usa para agregar nuevos registros a la tabla.
- **UPDATE**: Se usa para modificar registros existentes en la tabla.
- **DELETE**: Se usa para eliminar registros de la tabla.