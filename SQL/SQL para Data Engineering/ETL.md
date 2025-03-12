
## ETL con SQL (INSERT INTO SELECT, MERGE, UPSERT)

El proceso de **ETL** (Extract, Transform, Load) es fundamental en **Data Engineering**, y se utiliza para mover y transformar datos desde diversas fuentes hacia sistemas de almacenamiento o bases de datos para análisis y procesamiento. En SQL, varias operaciones permiten realizar estas transformaciones de manera eficiente.

### **INSERT INTO SELECT**

El comando `INSERT INTO SELECT` se utiliza para insertar datos de una tabla a otra, generalmente de una tabla fuente a una tabla destino. Este tipo de operación es muy útil cuando queremos **cargar** datos en una base de datos desde otra tabla o fuente de datos dentro del mismo sistema.

#### **Sintaxis:**
```sql
INSERT INTO tabla_destino (columna1, columna2, columna3)
SELECT columna1, columna2, columna3
FROM tabla_fuente
WHERE condiciones;
```

#### **Ejemplo:**

Imagina que tienes una tabla de ventas (`ventas_2022`) y deseas cargar esos datos en una tabla de archivo (`ventas_archivo`):

```sql
INSERT INTO ventas_archivo (id_venta, fecha, monto)
SELECT id_venta, fecha, monto
FROM ventas_2022
WHERE fecha > '2022-01-01';
```

Este comando selecciona las ventas de 2022 desde `ventas_2022` y las inserta en la tabla `ventas_archivo`.

### **MERGE (UPSERT)**

El comando `MERGE` es una operación más avanzada que se utiliza para **actualizar, insertar o eliminar datos** en una tabla destino según condiciones específicas basadas en los datos de la tabla de origen. En otras palabras, un **UPSERT** (una combinación de **UPDATE** y **INSERT**) permite realizar la actualización de registros existentes y la inserción de nuevos registros en una sola operación.

#### **Sintaxis:**
```sql
MERGE INTO tabla_destino AS destino
USING tabla_fuente AS fuente
ON destino.columna_id = fuente.columna_id
WHEN MATCHED THEN
    UPDATE SET destino.columna1 = fuente.columna1, destino.columna2 = fuente.columna2
WHEN NOT MATCHED THEN
    INSERT (columna1, columna2) VALUES (fuente.columna1, fuente.columna2);
```

#### **Ejemplo:**

Supón que tienes una tabla de clientes (`clientes_nueva`) con los datos más recientes y deseas actualizarlos en la tabla `clientes` existente. Si un cliente ya existe, se actualiza; si no, se inserta.

```sql
MERGE INTO clientes AS destino
USING clientes_nueva AS fuente
ON destino.id_cliente = fuente.id_cliente
WHEN MATCHED THEN
    UPDATE SET destino.nombre = fuente.nombre, destino.email = fuente.email
WHEN NOT MATCHED THEN
    INSERT (id_cliente, nombre, email) VALUES (fuente.id_cliente, fuente.nombre, fuente.email);
```

### **UPSERT (INSERT ON DUPLICATE KEY UPDATE)**

Algunos sistemas de bases de datos, como MySQL, permiten un enfoque específico para hacer **UPSERT** con la instrucción `INSERT ON DUPLICATE KEY UPDATE`. Esto es útil cuando intentas insertar un registro, pero si ya existe un conflicto (como una clave primaria duplicada), se actualiza en lugar de insertar un nuevo registro.

#### **Sintaxis:**
```sql
INSERT INTO tabla (columna1, columna2)
VALUES (valor1, valor2)
ON DUPLICATE KEY UPDATE
    columna1 = valor1, columna2 = valor2;
```

#### **Ejemplo:**

Si intentas insertar un nuevo cliente en una tabla `clientes`, pero si ya existe un cliente con el mismo `id_cliente`, actualizas sus datos:

```sql
INSERT INTO clientes (id_cliente, nombre, email)
VALUES (1, 'Juan Pérez', 'juan@example.com')
ON DUPLICATE KEY UPDATE
    nombre = 'Juan Pérez', email = 'juan@example.com';
```

### **Ventajas del uso de MERGE y UPSERT**

- **Eficiencia**: Reduce el número de consultas necesarias para insertar o actualizar datos, optimizando el tiempo de procesamiento.
- **Menos complejidad**: Combina múltiples pasos (insertar y actualizar) en una sola operación, lo que simplifica el código.
- **Control**: Permite una mayor flexibilidad, ya que puedes especificar qué hacer cuando los datos coinciden o no coinciden.

### **Consideraciones al usar MERGE y UPSERT**
- **Rendimiento**: Aunque `MERGE` y `UPSERT` son muy útiles, en bases de datos con grandes volúmenes de datos, estas operaciones pueden ser más costosas que las simples inserciones.
- **Compatibilidad**: No todos los sistemas de bases de datos soportan la misma sintaxis para `MERGE` o `UPSERT`. Por ejemplo, `MERGE` es compatible con SQL Server y Oracle, mientras que en MySQL se usa `INSERT ON DUPLICATE KEY UPDATE`.

---

### **Conclusión**

Las operaciones de **ETL con SQL** (como `INSERT INTO SELECT`, `MERGE` y **UPSERT**) son esenciales para la manipulación de datos en el contexto de **Data Engineering**. Estas herramientas permiten transformar y cargar grandes volúmenes de datos de manera eficiente, ya sea insertando, actualizando o combinando datos de múltiples fuentes. Conocer cómo utilizar estas operaciones de manera efectiva es crucial para diseñar y mantener procesos de integración de datos en sistemas de bases de datos.

