
### 1. **CREATE VIEW, DROP VIEW**

Las vistas son consultas almacenadas que se comportan como tablas virtuales. Se utilizan para simplificar las consultas complejas o para restringir el acceso a ciertas columnas o filas de una tabla.

---

#### **CREATE VIEW**

La sentencia **CREATE VIEW** se utiliza para crear una vista. Una vista es una consulta que se guarda en la base de datos, y puedes usarla como si fuera una tabla. A menudo se emplea para simplificar consultas complejas o para mostrar solo una parte de los datos a los usuarios.

##### Sintaxis:

```sql
CREATE VIEW nombre_vista AS
SELECT columnas
FROM tabla
WHERE condiciones;
```

##### Ejemplo:

Supongamos que tenemos una tabla llamada **Empleados** con las columnas **id**, **nombre**, **salario** y **departamento**. Si queremos crear una vista que muestre solo los empleados del departamento de ventas con un salario mayor a 5000:

```sql
CREATE VIEW Vista_Ventas AS
SELECT nombre, salario
FROM Empleados
WHERE departamento = 'Ventas' AND salario > 5000;
```

Esta vista, **Vista_Ventas**, mostrará solo los **nombre** y **salario** de los empleados que cumplen con las condiciones mencionadas (departamento = 'Ventas' y salario > 5000).

---

#### **DROP VIEW**

La sentencia **DROP VIEW** se usa para eliminar una vista existente. Una vez que se elimina la vista, ya no puede ser utilizada en futuras consultas.

##### Sintaxis:

```sql
DROP VIEW nombre_vista;
```

##### Ejemplo:

```sql
DROP VIEW Vista_Ventas;
```

Este comando elimina la vista **Vista_Ventas** de la base de datos.

---

### Ventajas de las Vistas:

1. **Simplicidad**: Las vistas permiten simplificar consultas complejas al almacenar la lógica de la consulta.
2. **Seguridad**: Se pueden usar vistas para restringir el acceso a datos sensibles. Por ejemplo, puedes crear una vista que solo muestre ciertos campos (como excluir datos confidenciales).
3. **Reusabilidad**: Una vez creada, una vista puede ser reutilizada múltiples veces en otras consultas sin tener que escribir la misma lógica una y otra vez.

---

### Resumen de **CREATE VIEW** y **DROP VIEW**:

- **CREATE VIEW**: Crea una vista que representa una consulta almacenada en la base de datos.
- **DROP VIEW**: Elimina una vista de la base de datos.

