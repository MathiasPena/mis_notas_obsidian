
Los **Procedimientos Almacenados** y los **Triggers** son objetos de la base de datos que permiten automatizar tareas, mejorar el rendimiento y asegurar que ciertas reglas se apliquen cuando se realizan operaciones en la base de datos.

---

#### **STORED PROCEDURES**

Un **procedimiento almacenado** es un conjunto de instrucciones SQL que se agrupan y se almacenan en la base de datos para ser ejecutadas de forma repetida. Los procedimientos almacenados pueden aceptar parámetros, lo que les permite ser reutilizados con diferentes entradas.

##### Sintaxis:

```sql
CREATE PROCEDURE nombre_procedimiento
@parametro1 tipo1,
@parametro2 tipo2
AS
BEGIN
  -- instrucciones SQL
END;
```

##### Ejemplo:

Supongamos que tenemos una tabla llamada **Empleados** y queremos crear un procedimiento almacenado para actualizar el salario de un empleado en función de su **id**:

```sql
CREATE PROCEDURE ActualizarSalario(@id INT, @nuevo_salario DECIMAL)
AS
BEGIN
  UPDATE Empleados
  SET salario = @nuevo_salario
  WHERE id = @id;
END;
```

Este procedimiento **ActualizarSalario** recibe dos parámetros: **id** y **nuevo_salario**. Cuando se ejecuta el procedimiento, actualiza el salario del empleado con el **id** especificado.

##### Ejecutar el procedimiento:

```sql
EXEC ActualizarSalario 1, 6000;
```

Este comando ejecuta el procedimiento almacenado **ActualizarSalario**, actualizando el salario del empleado con **id = 1** a 6000.

---

#### **TRIGGERS**

Un **trigger** (o desencadenador) es un tipo especial de procedimiento almacenado que se ejecuta automáticamente en respuesta a ciertos eventos en la base de datos, como **INSERT**, **UPDATE** o **DELETE**. Los triggers son útiles para la validación de datos, auditoría o mantener la integridad referencial sin necesidad de intervención manual.

##### Sintaxis:

```sql
CREATE TRIGGER nombre_trigger
AFTER INSERT | UPDATE | DELETE
ON nombre_tabla
FOR EACH ROW
BEGIN
  -- instrucciones SQL
END;
```

##### Ejemplo:

Supongamos que queremos crear un **trigger** que registre automáticamente en una tabla de auditoría cada vez que se actualice el salario de un empleado. Para esto, tenemos una tabla llamada **AuditoriaSalarios** con las columnas **id_empleado**, **antiguo_salario**, **nuevo_salario** y **fecha**.

```sql
CREATE TRIGGER TriggerAuditoriaSalario
AFTER UPDATE ON Empleados
FOR EACH ROW
BEGIN
  INSERT INTO AuditoriaSalarios(id_empleado, antiguo_salario, nuevo_salario, fecha)
  VALUES(OLD.id, OLD.salario, NEW.salario, NOW());
END;
```

Este **trigger** se ejecuta **después de una actualización** en la tabla **Empleados**. Usa las palabras clave **OLD** y **NEW** para acceder a los valores antes y después de la actualización. Cuando se actualiza el salario de un empleado, el **trigger** inserta automáticamente los valores antiguos y nuevos en la tabla **AuditoriaSalarios** junto con la fecha y hora de la actualización.

---

### Resumen de **STORED PROCEDURES** y **TRIGGERS**:

- **STORED PROCEDURE**: Es un conjunto de instrucciones SQL que se almacenan y pueden ser ejecutadas repetidamente con diferentes parámetros. Permite realizar operaciones complejas de manera eficiente y reutilizable.
- **TRIGGER**: Es un procedimiento que se ejecuta automáticamente en respuesta a eventos **INSERT**, **UPDATE** o **DELETE** sobre una tabla específica. Se usa para mantener la integridad de los datos, realizar auditorías o implementar reglas de negocio automáticamente.

