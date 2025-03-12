
**DDL (Data Definition Language)** es una parte de SQL que se utiliza para definir y modificar la estructura de las bases de datos y sus objetos, como tablas, índices y esquemas. A diferencia de DML (Data Manipulation Language), que manipula los datos dentro de las tablas, DDL se enfoca en la creación, modificación y eliminación de las estructuras de la base de datos.

## **1. CREATE** - Crear Objetos en la Base de Datos

El comando **`CREATE`** se utiliza para crear bases de datos, tablas, índices, vistas, y otros objetos dentro de la base de datos.

### Crear una tabla:
```sql
CREATE TABLE nombre_tabla (
    columna1 tipo_dato restricciones,
    columna2 tipo_dato restricciones,
    ...
);
```

### Ejemplo:
```sql
CREATE TABLE empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(100),
    salario DECIMAL(10, 2),
    fecha_ingreso DATE
);
```

### Crear una base de datos:
```sql
CREATE DATABASE empresa;
```

## **2. ALTER** - Modificar Objetos Existentes

El comando **`ALTER`** se usa para modificar la estructura de un objeto existente, como agregar, eliminar o cambiar columnas de una tabla.

### Sintaxis básica para agregar una columna:
```sql
ALTER TABLE nombre_tabla
ADD columna tipo_dato;
```

### Sintaxis básica para modificar una columna:
```sql
ALTER TABLE nombre_tabla
MODIFY columna tipo_dato;
```

### Sintaxis básica para eliminar una columna:
```sql
ALTER TABLE nombre_tabla
DROP COLUMN columna;
```

### Ejemplo (agregar una columna):
```sql
ALTER TABLE empleados
ADD direccion VARCHAR(200);
```

### Ejemplo (modificar una columna):
```sql
ALTER TABLE empleados
MODIFY salario DECIMAL(12, 2);
```

### Ejemplo (eliminar una columna):
```sql
ALTER TABLE empleados
DROP COLUMN direccion;
```

## **3. DROP** - Eliminar Objetos de la Base de Datos

El comando **`DROP`** se utiliza para eliminar completamente una tabla, una base de datos o cualquier otro objeto de la base de datos. **¡Ten cuidado!** Esto elimina tanto la estructura como los datos.

### Sintaxis básica para eliminar una tabla:
```sql
DROP TABLE nombre_tabla;
```

### Sintaxis básica para eliminar una base de datos:
```sql
DROP DATABASE nombre_base_datos;
```

### Ejemplo (eliminar una tabla):
```sql
DROP TABLE empleados;
```

### Ejemplo (eliminar una base de datos):
```sql
DROP DATABASE empresa;
```

## **4. TRUNCATE** - Eliminar Todos los Datos de una Tabla

El comando **`TRUNCATE`** se utiliza para eliminar todos los registros de una tabla de forma rápida y eficiente. A diferencia de **`DELETE`**, **`TRUNCATE`** no elimina la estructura de la tabla, solo los datos. **`TRUNCATE`** generalmente es más rápido porque no registra cada eliminación individualmente.

### Sintaxis básica:
```sql
TRUNCATE TABLE nombre_tabla;
```

### Ejemplo:
```sql
TRUNCATE TABLE empleados;
```

## **Conclusión**

Los comandos **DDL** (CREATE, ALTER, DROP y TRUNCATE) son esenciales para definir y gestionar la estructura de una base de datos. **`CREATE`** permite crear nuevos objetos, **`ALTER`** modifica la estructura de los existentes, **`DROP`** elimina objetos, y **`TRUNCATE`** elimina rápidamente los datos sin eliminar la tabla. Estos comandos son fundamentales para la administración de bases de datos, pero deben usarse con precaución, ya que pueden modificar o eliminar permanentemente los objetos y datos de la base de datos.
