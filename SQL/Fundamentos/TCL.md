
**TCL (Transaction Control Language)** es un conjunto de comandos SQL utilizados para gestionar transacciones en una base de datos. Estos comandos permiten controlar el flujo de las transacciones, asegurando que las operaciones se ejecuten de manera correcta y consistente. Los tres principales comandos TCL son **`COMMIT`**, **`ROLLBACK`**, y **`SAVEPOINT`**.

## **1. COMMIT** - Confirmar Transacción

El comando **`COMMIT`** se utiliza para guardar de forma permanente todos los cambios realizados en la base de datos durante una transacción. Una vez que se ejecuta **`COMMIT`**, los cambios se hacen permanentes y no pueden ser deshechos.

### Sintaxis básica:
```sql
COMMIT;
```

### Ejemplo:
```sql
BEGIN;

UPDATE empleados SET salario = salario * 1.1 WHERE departamento = 'Ventas';

COMMIT;
```
En este caso, todos los cambios realizados en la tabla **empleados** (incrementando el salario en un 10% para el departamento de ventas) se guardan permanentemente después de ejecutar **`COMMIT`**.

## **2. ROLLBACK** - Deshacer Transacción

El comando **`ROLLBACK`** se utiliza para deshacer los cambios realizados en una transacción. Si ocurre un error o si se desea cancelar la transacción por alguna razón, **`ROLLBACK`** revierte todas las modificaciones realizadas desde el último **`COMMIT`** o desde el último **`SAVEPOINT`**.

### Sintaxis básica:
```sql
ROLLBACK;
```

### Ejemplo:
```sql
BEGIN;

UPDATE empleados SET salario = salario * 1.1 WHERE departamento = 'Ventas';

-- Algo salió mal, deshacer cambios
ROLLBACK;
```
En este ejemplo, si ocurre un error o si se decide revertir la operación, **`ROLLBACK`** deshará el cambio y el salario no se incrementará.

## **3. SAVEPOINT** - Establecer un Punto de Guardado

El comando **`SAVEPOINT`** se utiliza para crear un punto de guardado dentro de una transacción. Permite revertir parcialmente una transacción hasta un punto específico, sin tener que deshacer toda la transacción. Esto es útil cuando se desea deshacer solo una parte de la transacción.

### Sintaxis básica:
```sql
SAVEPOINT nombre_punto;
```

### Ejemplo:
```sql
BEGIN;

UPDATE empleados SET salario = salario * 1.1 WHERE departamento = 'Ventas';

SAVEPOINT punto1;

UPDATE empleados SET salario = salario * 1.2 WHERE departamento = 'Marketing';

-- Si algo sale mal en Marketing, deshacer hasta el SAVEPOINT
ROLLBACK TO punto1;
```
En este ejemplo, si la actualización del salario para el departamento de **Marketing** falla, la transacción se puede revertir a **`punto1`** sin afectar los cambios realizados para el departamento de **Ventas**.

## **Conclusión**

Los comandos **TCL** permiten controlar el comportamiento de las transacciones en SQL, lo que es crucial para mantener la integridad de la base de datos. 
- **`COMMIT`** garantiza que los cambios sean permanentes.
- **`ROLLBACK`** permite deshacer los cambios de una transacción si algo sale mal.
- **`SAVEPOINT`** permite crear puntos de control dentro de una transacción, facilitando la reversión parcial de cambios.

El uso adecuado de estos comandos ayuda a asegurar que las operaciones de la base de datos sean confiables y que los errores se manejen de manera adecuada.
