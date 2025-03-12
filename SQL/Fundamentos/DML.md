# DML (Data Manipulation Language): SELECT, INSERT, UPDATE, DELETE

**DML (Data Manipulation Language)** es una parte de SQL que permite manipular los datos dentro de las tablas de una base de datos. Se usa para consultar, insertar, actualizar y eliminar datos.

## **1. SELECT** - Consultar Datos

El comando **`SELECT`** se usa para consultar y obtener datos de una o más tablas. Se pueden aplicar filtros, ordenar los resultados y realizar cálculos sobre los datos.

### Sintaxis básica:
```sql
SELECT columna1, columna2, ...
FROM tabla;
```

- **`SELECT *`**: Selecciona todas las columnas de la tabla.
- **`WHERE`**: Filtra los resultados según una condición.
- **`ORDER BY`**: Ordena los resultados.
- **`LIMIT`**: Limita la cantidad de registros devueltos.

### Ejemplo:
```sql
SELECT nombre, salario
FROM empleados
WHERE salario > 50000
ORDER BY salario DESC;
```

## **2. INSERT** - Insertar Datos

El comando **`INSERT`** se usa para agregar nuevos registros a una tabla.

### Sintaxis básica:
```sql
INSERT INTO tabla (columna1, columna2, ...)
VALUES (valor1, valor2, ...);
```

### Ejemplo:
```sql
INSERT INTO empleados (nombre, salario)
VALUES ('Juan Pérez', 55000);
```

Si se insertan valores para todas las columnas:
```sql
INSERT INTO empleados
VALUES (NULL, 'Ana Gómez', 48000);
```

## **3. UPDATE** - Actualizar Datos

El comando **`UPDATE`** se utiliza para modificar datos existentes en una tabla. Es importante usar **`WHERE`** para especificar qué registros se deben actualizar, de lo contrario, se actualizarán todos los registros.

### Sintaxis básica:
```sql
UPDATE tabla
SET columna1 = valor1, columna2 = valor2, ...
WHERE condición;
```

### Ejemplo:
```sql
UPDATE empleados
SET salario = 60000
WHERE nombre = 'Juan Pérez';
```

## **4. DELETE** - Eliminar Datos

El comando **`DELETE`** se usa para eliminar registros de una tabla. Similar a **`UPDATE`**, es importante usar **`WHERE`** para evitar eliminar todos los registros.

### Sintaxis básica:
```sql
DELETE FROM tabla
WHERE condición;
```

### Ejemplo:
```sql
DELETE FROM empleados
WHERE nombre = 'Ana Gómez';
```

Si se omite la condición **`WHERE`**, se eliminarán todos los registros de la tabla:
```sql
DELETE FROM empleados;
```

## **Conclusión**

Los comandos **DML** (SELECT, INSERT, UPDATE y DELETE) son fundamentales para interactuar con los datos en una base de datos. Cada uno tiene su función específica y se debe usar cuidadosamente para manipular los datos de forma precisa y eficiente. Recuerda siempre utilizar **`WHERE`** en **`UPDATE`** y **`DELETE`** para evitar cambios no deseados en todos los registros.
