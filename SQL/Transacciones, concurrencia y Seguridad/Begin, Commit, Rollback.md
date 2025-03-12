## Transacciones y Seguridad

### 1. **BEGIN, COMMIT, ROLLBACK**

Las transacciones en SQL permiten ejecutar un conjunto de operaciones de manera atómica. Esto significa que todas las operaciones dentro de una transacción deben completarse correctamente, o ninguna se aplica. Estas tres sentencias son esenciales para manejar transacciones:

---

#### **BEGIN**

La sentencia **BEGIN** se utiliza para iniciar una transacción en SQL. Una transacción comienza explícitamente con **BEGIN** (aunque algunas bases de datos manejan esto implícitamente cuando se realiza una operación de escritura).

##### Sintaxis:

```sql
BEGIN;
```

##### Ejemplo:

```sql
BEGIN;
UPDATE Empleados SET salario = salario * 1.1 WHERE id = 1;
UPDATE Empleados SET salario = salario * 1.1 WHERE id = 2;
```

En este ejemplo, comenzamos una transacción con **BEGIN**. Si ambas actualizaciones se completan correctamente, podemos confirmar la transacción con **COMMIT**. Si ocurre un error, podemos deshacerla con **ROLLBACK**.

---

#### **COMMIT**

La sentencia **COMMIT** se utiliza para confirmar una transacción. Después de ejecutar **COMMIT**, todas las operaciones realizadas dentro de la transacción se hacen permanentes y no se pueden revertir.

##### Sintaxis:

```sql
COMMIT;
```

##### Ejemplo:

```sql
BEGIN;
UPDATE Empleados SET salario = salario * 1.1 WHERE id = 1;
UPDATE Empleados SET salario = salario * 1.1 WHERE id = 2;
COMMIT;
```

En este caso, después de ejecutar ambas actualizaciones, confirmamos la transacción con **COMMIT**. Esto asegura que los cambios sean permanentes.

---

#### **ROLLBACK**

La sentencia **ROLLBACK** se utiliza para deshacer todas las operaciones realizadas en la transacción desde que comenzó. Si ocurre algún error o si no queremos que los cambios se guarden, podemos usar **ROLLBACK** para revertir la transacción.

##### Sintaxis:

```sql
ROLLBACK;
```

##### Ejemplo:

```sql
BEGIN;
UPDATE Empleados SET salario = salario * 1.1 WHERE id = 1;
UPDATE Empleados SET salario = salario * 1.1 WHERE id = 2;
-- Aquí, si ocurre un error o queremos deshacer los cambios:
ROLLBACK;
```

En este ejemplo, si algo sale mal en las actualizaciones o si decidimos revertir, usamos **ROLLBACK** para deshacer los cambios hechos dentro de la transacción.

---

### Resumen de las Transacciones:

1. **BEGIN**: Inicia una transacción.
2. **COMMIT**: Confirma todos los cambios realizados en la transacción y los hace permanentes.
3. **ROLLBACK**: Revierte todos los cambios realizados en la transacción y los deshace.

Las transacciones aseguran la **atomicidad** de las operaciones, es decir, que todas las operaciones dentro de una transacción se completan correctamente o ninguna se aplica.

