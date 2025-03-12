
## Bloqueos y Concurrencia (READ COMMITTED, SERIALIZABLE)

Cuando varias transacciones se ejecutan de manera simultánea en una base de datos, puede haber problemas relacionados con la **concurrencia** de las transacciones. Para evitar problemas como lecturas inconsistentes, actualizaciones perdidas o "fantasmas", las bases de datos implementan **bloqueos** y diferentes **niveles de aislamiento** de las transacciones.

### **Lecturas Sucias (Dirty Reads)**

Un **Dirty Read** ocurre cuando una transacción lee datos que han sido modificados por otra transacción, pero aún no han sido confirmados (commit). Esto puede llevar a inconsistencias si la transacción que realizó los cambios finalmente se revierte (rollback).

### **Fantasmas (Phantom Reads)**

Un **Phantom Read** se produce cuando una transacción lee un conjunto de filas que cambian por otra transacción mientras está en curso. El resultado es que los datos leídos por la transacción inicial podrían ser diferentes si se leen nuevamente.

### **Niveles de Aislamiento**

Los niveles de aislamiento controlan el grado en que una transacción puede ver los cambios realizados por otras transacciones que aún no han sido confirmadas. Existen varios niveles de aislamiento definidos por el estándar SQL, que ayudan a evitar problemas de concurrencia.

#### **1. READ UNCOMMITTED (Lectura No Confirmada)**

En este nivel, las transacciones pueden leer datos modificados por otras transacciones que no han sido confirmadas (es decir, pueden ocurrir **Dirty Reads**).

- **Problema**: **Dirty Reads** y **Fantasmas**.
- **Uso**: Muy poco seguro, pero puede ser útil en entornos donde la precisión no es crítica.

```sql
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
```

#### **2. READ COMMITTED (Lectura Confirmada)**

El nivel **READ COMMITTED** asegura que una transacción solo pueda leer datos que han sido confirmados por otras transacciones. Esto evita los **Dirty Reads**, pero no garantiza que los datos leídos no cambien durante la ejecución de la transacción (es decir, **Non-repeatable Reads** pueden ocurrir).

- **Problema**: **Non-repeatable Reads** (lecturas no repetibles).
- **Uso**: Es el nivel de aislamiento predeterminado en muchas bases de datos, como PostgreSQL y SQL Server.

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

#### **3. REPEATABLE READ (Lectura Repetible)**

En este nivel, las transacciones garantizan que los datos que han sido leídos no pueden cambiar durante el curso de la transacción. Esto previene tanto **Dirty Reads** como **Non-repeatable Reads**. Sin embargo, todavía se pueden producir **Fantasmas**.

- **Problema**: **Fantasmas**.
- **Uso**: Utilizado cuando es crucial que los datos leídos sean consistentes durante toda la transacción.

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```

#### **4. SERIALIZABLE (Serializable)**

El nivel más alto de aislamiento es **SERIALIZABLE**. Este nivel asegura que las transacciones se ejecuten de manera secuencial (una después de la otra) como si fueran transacciones completamente serializadas. Esto previene todos los problemas de concurrencia, incluyendo **Dirty Reads**, **Non-repeatable Reads** y **Fantasmas**. Sin embargo, este nivel puede reducir significativamente el rendimiento debido a los bloqueos más estrictos.

- **Problema**: El rendimiento puede verse afectado por el alto costo de los bloqueos.
- **Uso**: Se utiliza cuando es crucial mantener la integridad completa de los datos, como en operaciones bancarias y financieras.

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

### **Bloqueos (Locks)**

En el contexto de transacciones y concurrencia, los **bloqueos** son mecanismos utilizados por las bases de datos para asegurar que los datos no sean modificados por múltiples transacciones de manera simultánea de forma que se genere inconsistencia.

- **Bloqueo exclusivo (Exclusive Lock)**: Previene que otras transacciones lean o escriban en el recurso bloqueado.
- **Bloqueo compartido (Shared Lock)**: Permite que otras transacciones lean el recurso, pero no lo modifiquen.

Cuando se usa un alto nivel de aislamiento como **SERIALIZABLE**, la base de datos puede aplicar bloqueos más estrictos (bloqueos exclusivos) para garantizar que las transacciones no interfieran entre sí.

### **Conclusión**

- **READ COMMITTED** es el nivel de aislamiento más común y asegura que las transacciones solo lean datos confirmados, pero puede permitir **Non-repeatable Reads**.
- **SERIALIZABLE** ofrece el mayor nivel de protección contra problemas de concurrencia, pero puede afectar negativamente al rendimiento debido a bloqueos más estrictos y la serialización de las transacciones.
- El uso de diferentes niveles de aislamiento depende de la naturaleza de las transacciones y la necesidad de garantizar la integridad de los datos frente a las preocupaciones de rendimiento.
