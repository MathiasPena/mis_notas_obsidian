
Estas son las sentencias SQL básicas para crear, modificar y eliminar tablas en una base de datos.

---

#### **CREATE TABLE**

La sentencia **CREATE TABLE** se usa para crear una nueva tabla en la base de datos. Puedes especificar el nombre de la tabla y las columnas con sus tipos de datos y restricciones.

##### Sintaxis:

```sql
CREATE TABLE nombre_tabla (
    columna1 tipo_dato [restricciones],
    columna2 tipo_dato [restricciones],
    ...
);
```

##### Ejemplo:

```sql
CREATE TABLE Empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(100),
    salario DECIMAL(10, 2),
    fecha_ingreso DATE
);
```

En este caso, estamos creando una tabla llamada **Empleados** con cuatro columnas: **id**, **nombre**, **salario**, y **fecha_ingreso**.

---

#### **ALTER TABLE**

La sentencia **ALTER TABLE** se usa para modificar una tabla existente. Puedes agregar, eliminar o modificar columnas, o incluso cambiar las restricciones de una tabla.

##### Sintaxis:

- **Agregar una columna**:

```sql
ALTER TABLE nombre_tabla
ADD columna tipo_dato [restricciones];
```

- **Eliminar una columna**:

```sql
ALTER TABLE nombre_tabla
DROP COLUMN columna;
```

- **Modificar una columna**:

```sql
ALTER TABLE nombre_tabla
MODIFY COLUMN columna tipo_dato [restricciones];
```

##### Ejemplos:

- **Agregar una columna**:

```sql
ALTER TABLE Empleados
ADD telefono VARCHAR(15);
```

Este comando agrega una columna llamada **telefono** de tipo **VARCHAR(15)** a la tabla **Empleados**.

- **Eliminar una columna**:

```sql
ALTER TABLE Empleados
DROP COLUMN fecha_ingreso;
```

Este comando elimina la columna **fecha_ingreso** de la tabla **Empleados**.

- **Modificar una columna**:

```sql
ALTER TABLE Empleados
MODIFY COLUMN salario DECIMAL(12, 2);
```

Este comando cambia el tipo de la columna **salario** para permitir hasta 12 dígitos, con 2 decimales.

---

#### **DROP TABLE**

La sentencia **DROP TABLE** se usa para eliminar completamente una tabla de la base de datos. Esto elimina la tabla y todos los datos que contiene, por lo que debe usarse con precaución.

##### Sintaxis:

```sql
DROP TABLE nombre_tabla;
```

##### Ejemplo:

```sql
DROP TABLE Empleados;
```

Este comando elimina la tabla **Empleados** de la base de datos.

---

### Resumen:

- **CREATE TABLE**: Crea una nueva tabla en la base de datos.
- **ALTER TABLE**: Modifica una tabla existente, agregando, eliminando o modificando columnas.
- **DROP TABLE**: Elimina completamente una tabla y sus datos.