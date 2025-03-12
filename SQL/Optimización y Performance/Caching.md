
## Estrategias de Caching (MATERIALIZED VIEWS, TEMPORARY TABLES)

La optimización de consultas en bases de datos es esencial para mejorar el rendimiento de las aplicaciones, especialmente cuando se manejan grandes volúmenes de datos. Una estrategia común para optimizar consultas es el uso de técnicas de **caching**, las cuales permiten almacenar resultados intermedios o precomputados para evitar recalcular los mismos datos repetidamente.

### **Materialized Views**

Una **Materialized View** (vista materializada) es una vista que almacena físicamente los resultados de una consulta en la base de datos, en lugar de recalcular la consulta cada vez que se invoca. Esto es útil cuando las consultas son costosas o involucran grandes volúmenes de datos que no cambian con frecuencia. Las vistas materializadas pueden mejorar significativamente el rendimiento de las consultas, ya que los datos ya están precomputados y listos para ser consultados.

#### Características:
- **Almacenamiento físico**: Los resultados de la consulta se almacenan como una tabla real en la base de datos.
- **Actualización manual**: Dependiendo de la configuración, puede ser necesario actualizar manualmente la vista materializada para reflejar los cambios en las tablas subyacentes.
- **Reducción de tiempo de ejecución**: Al eliminar la necesidad de recalcular los resultados de la consulta cada vez, se mejora el rendimiento de las consultas.

#### Sintaxis Básica:
```sql
CREATE MATERIALIZED VIEW nombre_vista AS
SELECT columna1, columna2
FROM tabla
WHERE condición;
```

**Ejemplo:**
```sql
CREATE MATERIALIZED VIEW mv_clientes_activos AS
SELECT id_cliente, nombre, email
FROM Clientes
WHERE estado = 'Activo';
```

Para actualizar la vista materializada (en bases de datos como PostgreSQL), se puede usar:
```sql
REFRESH MATERIALIZED VIEW mv_clientes_activos;
```

### **Temporary Tables**

Las **Temporary Tables** (tablas temporales) son tablas que solo existen durante la duración de la sesión o transacción actual. Son útiles cuando necesitas realizar cálculos intermedios o almacenar resultados de consultas de forma temporal para su posterior procesamiento, pero no necesitas almacenar esos datos de manera permanente. 

Las tablas temporales son eliminadas automáticamente al final de la sesión o cuando se cierra la conexión a la base de datos.

#### Características:
- **Persistencia limitada**: Las tablas temporales existen solo durante la sesión o transacción y son eliminadas automáticamente al finalizar.
- **Uso de recursos limitado**: Al ser temporales, se almacenan en memoria o en espacio temporal de la base de datos, lo que las hace más rápidas en términos de acceso.
- **Mejor rendimiento**: Pueden mejorar el rendimiento en consultas complejas que requieren almacenamiento temporal de resultados intermedios.

#### Sintaxis Básica:
```sql
CREATE TEMPORARY TABLE nombre_tabla_temp (
    columna1 tipo1,
    columna2 tipo2,
    ...
);
```

**Ejemplo:**
```sql
CREATE TEMPORARY TABLE temp_clientes_activos AS
SELECT id_cliente, nombre
FROM Clientes
WHERE estado = 'Activo';
```

Las tablas temporales se eliminan automáticamente cuando termina la sesión o puedes eliminarlas explícitamente con:
```sql
DROP TABLE temp_clientes_activos;
```

### **Comparación entre Materialized Views y Temporary Tables**

| Característica              | Materialized View                        | Temporary Table                         |
|-----------------------------|------------------------------------------|-----------------------------------------|
| **Persistencia**             | Los resultados se almacenan permanentemente, pero requieren actualización manual. | Solo existe durante la sesión o transacción. |
| **Actualización**            | Debe actualizarse explícitamente con `REFRESH`. | No requiere actualización.             |
| **Uso principal**            | Consultas que requieren almacenamiento precomputado para mejorar el rendimiento. | Cálculos temporales durante una sesión o transacción. |
| **Impacto en rendimiento**   | Mejora el rendimiento al evitar el cálculo repetido de datos costosos. | Mejora el rendimiento de operaciones complejas al almacenar resultados intermedios temporalmente. |
| **Espacio en disco**         | Ocupa espacio en disco, ya que los datos se almacenan físicamente. | No ocupa espacio en disco permanente, pero puede usar espacio temporal. |

### **Cuándo usar cada uno**

- **Materialized Views**: Son ideales cuando necesitas almacenar resultados de consultas complejas que no cambian frecuentemente y que se consultan muchas veces. Perfecto para cargas de trabajo que involucran grandes volúmenes de datos estáticos o poco cambiantes.
- **Temporary Tables**: Son mejores cuando necesitas almacenar resultados intermedios durante una consulta compleja o una serie de operaciones, sin la necesidad de mantener esos datos después de completar la tarea.

---

### **Resumen**

- **Materialized Views**: Almacenan físicamente los resultados de una consulta y mejoran el rendimiento de consultas costosas al evitar recalcular los resultados. Requieren actualización manual.
- **Temporary Tables**: Son útiles para almacenar datos temporales durante una sesión o transacción y pueden acelerar las consultas complejas que requieren resultados intermedios sin necesidad de almacenamiento persistente.

Ambas estrategias son útiles para optimizar consultas en bases de datos, pero deben elegirse según el contexto y la necesidad de persistencia de los datos.

