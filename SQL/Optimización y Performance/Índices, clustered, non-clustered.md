## Optimización y Performance

### 1. **Índices**

Un **índice** es una estructura de datos que mejora la velocidad de las operaciones de consulta en una base de datos. Los índices permiten acceder a los datos de manera más eficiente, lo que es especialmente útil para tablas grandes con muchas filas.

#### **¿Qué es un índice?**

Un índice en una base de datos es similar a un índice en un libro: te permite buscar rápidamente una información específica sin tener que recorrer todo el contenido. En una base de datos, los índices se crean sobre una o más columnas de una tabla.

#### **Tipos de Índices:**

1. **Índice simple**: Se crea sobre una sola columna.
2. **Índice compuesto**: Se crea sobre dos o más columnas.
3. **Índice único**: No permite valores duplicados en las columnas indexadas.
4. **Índice de texto completo**: Utilizado para búsquedas de texto en grandes cantidades de datos de tipo texto.

#### **CREATE INDEX**

La sentencia **CREATE INDEX** se utiliza para crear un índice en una tabla. El índice puede estar basado en una o más columnas.

##### Sintaxis:

```sql
CREATE INDEX nombre_indice ON nombre_tabla (columna1, columna2, ...);
```

##### Ejemplo:

Supongamos que tenemos una tabla **Empleados** con las columnas **id**, **nombre** y **salario**. Si queremos crear un índice para la columna **nombre** (lo que acelerará las búsquedas por nombre):

```sql
CREATE INDEX idx_nombre ON Empleados(nombre);
```

Este índice **idx_nombre** acelera las consultas que filtren por **nombre**.

#### **Índices Únicos**

Los índices **únicos** aseguran que los valores de la columna o columnas que se indexan no se repitan. Esto es útil para garantizar la unicidad de los valores en una columna, como los **números de identificación de usuario**.

##### Ejemplo:

```sql
CREATE UNIQUE INDEX idx_unique_id ON Empleados(id);
```

Este índice asegura que los valores de la columna **id** sean únicos en la tabla **Empleados**.

#### **DROP INDEX**

La sentencia **DROP INDEX** se utiliza para eliminar un índice que ya no sea necesario.

##### Sintaxis:

```sql
DROP INDEX nombre_indice;
```

##### Ejemplo:

```sql
DROP INDEX idx_nombre;
```

Este comando elimina el índice **idx_nombre** de la tabla **Empleados**.

#### **Ventajas de los Índices**:

- **Mejora del rendimiento**: Los índices aceleran las búsquedas y las consultas de filtrado, lo que mejora significativamente el rendimiento de la base de datos, especialmente en tablas grandes.
- **Optimización de JOINs**: Los índices también pueden optimizar las operaciones de **JOIN** entre tablas, acelerando la combinación de datos.
- **Reducción de tiempo de búsqueda**: Al usar un índice, no es necesario recorrer todas las filas de una tabla para encontrar un valor.

#### **Desventajas de los Índices**:

- **Espacio adicional**: Los índices ocupan espacio adicional en la base de datos.
- **Rendimiento de escritura**: Las operaciones de inserción, actualización y eliminación pueden volverse más lentas debido a que los índices deben actualizarse cada vez que se modifican los datos.

---

### Resumen de **Índices**:

- Los **índices** son estructuras que mejoran la velocidad de las consultas y búsquedas en la base de datos.
- Se pueden crear índices simples o compuestos según las columnas utilizadas.
- Aseguran la **unicidad** de los valores en ciertas columnas (en el caso de índices únicos).
- Aunque mejoran las consultas, pueden afectar el rendimiento de las operaciones de escritura y requieren espacio adicional.


## Indexación Eficiente (CREATE INDEX, CLUSTERED, NON-CLUSTERED)

La **indexación** en bases de datos es una técnica utilizada para mejorar la velocidad de las operaciones de consulta (SELECT) al permitir búsquedas más rápidas en grandes volúmenes de datos. Los índices funcionan como índices en un libro: ayudan a localizar datos sin necesidad de revisar toda la tabla. Sin embargo, la indexación también introduce una sobrecarga en las operaciones de **INSERT**, **UPDATE** y **DELETE**, ya que los índices deben mantenerse actualizados.

### **CREATE INDEX**

El comando **CREATE INDEX** se utiliza para crear un índice en una o más columnas de una tabla, lo que acelera las búsquedas que involucran esas columnas. Existen varios tipos de índices, pero los más comunes son los **clustered** y **non-clustered**.

#### Sintaxis Básica:

```sql
CREATE INDEX nombre_del_indice
ON nombre_de_la_tabla (columna1, columna2, ...);
```

**Ejemplo:**

```sql
CREATE INDEX idx_nombre_cliente
ON Clientes(nombre);
```

Este índice mejora la velocidad de las consultas que busquen clientes por nombre en la tabla **Clientes**.

---

### **Índices Clustered**

Un **índice clustered** organiza físicamente los datos en la tabla de acuerdo con el orden del índice. Solo puede haber un índice **clustered** por tabla, ya que los datos de la tabla solo se pueden ordenar de una forma. El índice **clustered** afecta directamente la disposición física de los datos en el disco.

Cuando se crea una clave primaria, automáticamente se crea un índice **clustered**.

#### Características:
- Los datos de la tabla están organizados de acuerdo con el índice.
- Solo puede haber un índice **clustered** en una tabla.
- Es ideal para consultas que involucran rangos de datos o que se ordenan por la columna indexada.

#### Ejemplo:
```sql
CREATE CLUSTERED INDEX idx_cliente_id
ON Clientes(cliente_id);
```

Este índice reorganiza físicamente la tabla **Clientes** según el **cliente_id**, lo que hace más eficientes las búsquedas basadas en este campo.

---

### **Índices Non-Clustered**

A diferencia de los índices **clustered**, los **non-clustered** no afectan la organización física de los datos en la tabla. Un índice **non-clustered** crea una estructura de árbol B (B-tree) que apunta a las filas de la tabla. En una tabla puede haber múltiples índices **non-clustered**, lo que permite optimizar diferentes tipos de consultas.

#### Características:
- No cambia la organización física de los datos en la tabla.
- Puede haber varios índices **non-clustered** en una tabla.
- Útil para consultas que no afectan el orden físico de los datos.

#### Ejemplo:
```sql
CREATE NONCLUSTERED INDEX idx_cliente_email
ON Clientes(email);
```

Este índice permite búsquedas rápidas de clientes por su **email** sin alterar la organización física de la tabla.

---

### **Elección entre Clustered y Non-Clustered**

- **Clustered**: Si necesitas mejorar el rendimiento de consultas que ordenan o filtran datos en base a una columna específica, es preferible un índice **clustered**.
- **Non-Clustered**: Si necesitas múltiples índices para consultas que utilizan diferentes columnas o no requieren un orden específico de los datos, los índices **non-clustered** son más adecuados.

### **Consideraciones para la Indexación:**
1. **Evitar la sobrecarga**: Si bien los índices mejoran las consultas SELECT, también agregan una sobrecarga en las operaciones de **INSERT**, **UPDATE** y **DELETE**, ya que deben actualizarse cada vez que se modifican los datos.
2. **Elegir columnas de consulta frecuente**: Crea índices en las columnas que se usan más frecuentemente en las condiciones de búsqueda (**WHERE**, **JOIN**, etc.).
3. **Uso de índices compuestos**: Si las consultas involucran más de una columna, puedes crear índices compuestos (índices sobre varias columnas) para optimizar la consulta.

#### Ejemplo de índice compuesto:

```sql
CREATE INDEX idx_cliente_nombre_email
ON Clientes(nombre, email);
```

Este índice es útil si las consultas frecuentemente filtran por **nombre** y **email** simultáneamente.

---

### **Resumen**

- **Índice Clustered**: Organiza físicamente los datos en la tabla y solo puede haber uno por tabla. Es ideal para consultas basadas en rangos o que ordenan por la columna indexada.
- **Índice Non-Clustered**: Crea una estructura separada que apunta a las filas de la tabla y puede haber múltiples índices en una tabla. Es útil para consultas en las que no se requiere un orden específico.
- La correcta implementación de índices puede mejorar considerablemente el rendimiento de las consultas, pero se debe tener en cuenta el impacto en las operaciones de modificación de datos (INSERT, UPDATE, DELETE).

