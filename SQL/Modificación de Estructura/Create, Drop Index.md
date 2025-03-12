
Los índices se utilizan para mejorar el rendimiento de las consultas, especialmente en tablas grandes. **CREATE INDEX** se usa para crear un índice en una o más columnas, mientras que **DROP INDEX** se usa para eliminar un índice.

---

#### **CREATE INDEX**

La sentencia **CREATE INDEX** se usa para crear un índice en una tabla. Esto mejora el rendimiento de las consultas **SELECT** que filtran, ordenan o buscan datos en las columnas indexadas.

##### Sintaxis:

```sql
CREATE INDEX nombre_indice ON nombre_tabla (columna1, columna2, ...);
```

##### Ejemplo:

```sql
CREATE INDEX idx_nombre_empleado ON Empleados (nombre);
```

Este comando crea un índice llamado **idx_nombre_empleado** en la columna **nombre** de la tabla **Empleados**. Esto acelera las búsquedas de empleados por nombre.

- **Índice compuesto** (índice sobre varias columnas):

```sql
CREATE INDEX idx_empleado_salario ON Empleados (nombre, salario);
```

Este índice se crea sobre las columnas **nombre** y **salario**, lo que mejora el rendimiento de las consultas que filtren por estas dos columnas.

---

#### **DROP INDEX**

La sentencia **DROP INDEX** se utiliza para eliminar un índice de la base de datos. Es útil si ya no necesitas el índice o si quieres liberar espacio.

##### Sintaxis:

```sql
DROP INDEX nombre_indice;
```

##### Ejemplo:

```sql
DROP INDEX idx_nombre_empleado;
```

Este comando elimina el índice **idx_nombre_empleado** de la tabla **Empleados**. Después de ejecutar este comando, las consultas que filtren por la columna **nombre** ya no se beneficiarán de un índice.

---

### Consideraciones sobre el uso de índices:

1. **Ventajas**:
   - Los índices mejoran el rendimiento de las consultas **SELECT** en columnas indexadas.
   - Son especialmente útiles cuando hay muchas filas y se realizan búsquedas, ordenamientos o filtrados frecuentes.

2. **Desventajas**:
   - Los índices pueden afectar el rendimiento de las operaciones de **INSERT**, **UPDATE** y **DELETE**, ya que el índice debe actualizarse cada vez que los datos en la tabla cambian.
   - Crear demasiados índices puede consumir espacio en disco.

3. **Índices automáticos**:
   - Las bases de datos crean automáticamente índices en columnas **PRIMARY KEY** y **UNIQUE**, por lo que no es necesario crearlos manualmente.

---

### Resumen:

- **CREATE INDEX**: Crea un índice en una o más columnas de una tabla para mejorar el rendimiento de las consultas.
- **DROP INDEX**: Elimina un índice de la base de datos.

