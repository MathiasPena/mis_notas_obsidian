# Transacciones y Concurrencia

## ACID (Atomicidad, Consistencia, Aislamiento, Durabilidad)

Las bases de datos transaccionales deben garantizar que las operaciones sean fiables y consistentes, incluso en presencia de fallos o concurrencia de múltiples usuarios. Este conjunto de propiedades se conoce como **ACID**, que es el acrónimo de los cuatro principios fundamentales que aseguran la integridad de las transacciones en una base de datos.

### **1. Atomicidad**

La **Atomicidad** asegura que una transacción se ejecute de manera completa o no se ejecute en absoluto. Es decir, las transacciones se consideran como una "unidad atómica" que se realiza en su totalidad o no se realiza nada.

- **Ejemplo**: Si una transacción implica dos operaciones, como transferir dinero de una cuenta a otra, si alguna de las operaciones falla, ninguna de las dos se realiza (el dinero no se transfiere ni se pierde).

```sql
BEGIN TRANSACTION;

UPDATE cuenta SET saldo = saldo - 100 WHERE id = 1;  -- Descontar 100 de la cuenta 1
UPDATE cuenta SET saldo = saldo + 100 WHERE id = 2;  -- Agregar 100 a la cuenta 2

COMMIT;  -- Si ambas operaciones se realizan correctamente, la transacción se confirma
```

Si algo sale mal en cualquier parte de la transacción, se **deshacen** todas las operaciones realizadas hasta ese momento.

### **2. Consistencia**

La **Consistencia** garantiza que una transacción lleve la base de datos de un estado válido a otro estado válido. Después de que una transacción se complete, los datos deben cumplir con todas las reglas y restricciones de integridad definidas en la base de datos.

- **Ejemplo**: Si hay restricciones de clave foránea, una transacción que intente eliminar una fila referenciada por otra tabla fallará, lo que asegura que la base de datos no quede en un estado inconsistente.

### **3. Aislamiento**

El **Aislamiento** se refiere a la capacidad de una transacción de ejecutarse de forma independiente sin ser afectada por otras transacciones concurrentes. Esto significa que los cambios realizados en una transacción no deben ser visibles para otras transacciones hasta que la transacción haya sido confirmada (commit).

Los niveles de aislamiento varían, y las transacciones pueden estar sujetas a diferentes comportamientos de concurrencia según el nivel de aislamiento:

- **READ UNCOMMITTED**: Las transacciones pueden ver cambios no confirmados de otras transacciones.
- **READ COMMITTED**: Solo se pueden ver los cambios confirmados de otras transacciones.
- **REPEATABLE READ**: Asegura que los datos leídos no cambien durante la transacción.
- **SERIALIZABLE**: Garantiza la máxima protección, donde las transacciones se ejecutan como si fueran secuenciales.

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

BEGIN TRANSACTION;
    -- Operaciones de la transacción
COMMIT;
```

### **4. Durabilidad**

La **Durabilidad** asegura que una vez que una transacción ha sido confirmada (commit), los cambios realizados en la base de datos son permanentes, incluso si ocurre un fallo en el sistema (como una caída de energía).

- **Ejemplo**: Después de que una transacción se haya confirmado, los cambios son almacenados de forma segura en disco, lo que significa que no se perderán, incluso si el sistema se apaga inesperadamente.

### **Resumen de ACID**

- **Atomicidad**: Todo o nada, la transacción se completa por completo o no se realiza.
- **Consistencia**: La base de datos pasa de un estado válido a otro estado válido.
- **Aislamiento**: Las transacciones concurrentes no afectan la ejecución de otras.
- **Durabilidad**: Los cambios confirmados son permanentes, incluso si el sistema falla.

### **Ejemplo de transacción ACID en SQL**

```sql
BEGIN TRANSACTION;

-- Actualizar saldo de cuenta
UPDATE cuentas SET saldo = saldo - 500 WHERE cuenta_id = 1;

-- Comprobar saldo antes de actualizar la otra cuenta
IF (SELECT saldo FROM cuentas WHERE cuenta_id = 2) >= 500
BEGIN
    UPDATE cuentas SET saldo = saldo + 500 WHERE cuenta_id = 2;
    COMMIT;  -- Confirmar la transacción si todo ha ido bien
END
ELSE
BEGIN
    ROLLBACK;  -- Deshacer los cambios si no se cumple la condición
END
```

### **Conclusión**

Las propiedades ACID son fundamentales para garantizar que las bases de datos gestionen las transacciones de forma segura y confiable. El cumplimiento de estas propiedades es clave para mantener la integridad de los datos y asegurar que las aplicaciones puedan operar de manera coherente y segura en entornos con múltiples usuarios y concurrencia.
