# Consultas Avanzadas

## Subqueries y CTEs (WITH AS para mejorar legibilidad)

Las subconsultas y las **CTEs (Common Table Expressions)** son herramientas poderosas en SQL para mejorar la estructura y legibilidad de las consultas complejas. Ambas permiten estructurar las consultas de manera más modular, pero tienen diferencias en su uso y eficiencia.

## **1. Subqueries** - Subconsultas

Una **subconsulta** es una consulta dentro de otra consulta. Se puede usar en varias partes de la consulta principal, como en la cláusula **`WHERE`**, **`FROM`**, o **`SELECT`**. Las subconsultas pueden ser **correlacionadas** (cuando dependen de la consulta externa) o **no correlacionadas** (cuando son independientes).

### Sintaxis básica de una subconsulta en **`WHERE`**:
```sql
SELECT columna1
FROM tabla
WHERE columna1 = (SELECT columna2 FROM tabla2 WHERE condición);
```

### Ejemplo de subconsulta **no correlacionada**:
```sql
SELECT nombre
FROM empleados
WHERE salario > (SELECT AVG(salario) FROM empleados);
```
Este ejemplo devuelve los **nombres** de los empleados cuyo salario es mayor que el salario promedio de todos los empleados.

### Ejemplo de subconsulta **correlacionada**:
```sql
SELECT e.nombre
FROM empleados e
WHERE e.salario > (SELECT AVG(salario) FROM empleados WHERE departamento = e.departamento);
```
Este ejemplo devuelve los **nombres** de los empleados cuyo salario es mayor al salario promedio de su mismo departamento.

## **2. CTEs (Common Table Expressions)** - Expresiones de Tabla Común

Una **CTE** es una forma de estructurar las consultas SQL de manera más legible y modular. Se define con la palabra clave **`WITH`** y se utiliza para definir una consulta temporal que se puede referenciar en la consulta principal. Las CTEs son especialmente útiles cuando se necesita reutilizar una subconsulta en múltiples partes de la consulta principal.

### Sintaxis básica de una CTE:
```sql
WITH nombre_cte AS (
    SELECT columna1, columna2
    FROM tabla
    WHERE condición
)
SELECT *
FROM nombre_cte;
```

### Ejemplo de uso de CTE:
```sql
WITH salario_promedio AS (
    SELECT AVG(salario) AS promedio_salario
    FROM empleados
)
SELECT nombre
FROM empleados
WHERE salario > (SELECT promedio_salario FROM salario_promedio);
```
Este ejemplo primero calcula el salario promedio usando una **CTE** llamada `salario_promedio` y luego selecciona los empleados cuyo salario es mayor que ese promedio.

## **3. Comparativa entre Subqueries y CTEs**

### Subqueries:
- Se usan dentro de otras consultas.
- Pueden ser **correlacionadas** o **no correlacionadas**.
- Pueden ser menos legibles en consultas complejas.
- Generalmente se evalúan para cada fila en la consulta externa (lo que puede ser ineficiente en algunos casos).

### CTEs:
- Mejoran la legibilidad de consultas complejas.
- Se definen una sola vez y se pueden reutilizar en la consulta principal.
- Son más fáciles de entender y mantener en comparación con las subconsultas anidadas.
- Se pueden usar para resolver consultas recursivas.

## **4. CTEs Recursivas**

Las **CTEs recursivas** son un tipo especial de CTE que se utiliza para consultas que requieren navegar por datos jerárquicos o recursivos, como en el caso de árboles o jerarquías. Una CTE recursiva tiene dos partes: la parte ancla y la parte recursiva.

### Sintaxis básica de una CTE recursiva:
```sql
WITH RECURSIVE nombre_cte AS (
    -- Parte ancla
    SELECT columna1, columna2
    FROM tabla
    WHERE condición
    UNION ALL
    -- Parte recursiva
    SELECT t.columna1, t.columna2
    FROM tabla t
    JOIN nombre_cte cte ON t.columna1 = cte.columna2
)
SELECT *
FROM nombre_cte;
```

### Ejemplo de CTE recursiva:
```sql
WITH RECURSIVE jerarquia_empleados AS (
    -- Parte ancla: empleados que no tienen jefe
    SELECT id, nombre, jefe_id
    FROM empleados
    WHERE jefe_id IS NULL
    UNION ALL
    -- Parte recursiva: empleados cuyo jefe está en la jerarquía
    SELECT e.id, e.nombre, e.jefe_id
    FROM empleados e
    JOIN jerarquia_empleados j ON e.jefe_id = j.id
)
SELECT *
FROM jerarquia_empleados;
```
Este ejemplo crea una jerarquía de empleados comenzando desde los empleados sin jefe y luego siguiendo la relación de **jefe-subordinado** de manera recursiva.

## **Conclusión**

- Las **subconsultas** son útiles para consultas rápidas y simples, pero pueden volverse difíciles de mantener en consultas complejas.
- Las **CTEs** mejoran la legibilidad y modularidad de las consultas, y son especialmente útiles cuando se necesita reutilizar la misma subconsulta en varias partes de la consulta principal.
- Las **CTEs recursivas** son ideales para trabajar con datos jerárquicos o recursivos.

El uso de **subconsultas** o **CTEs** depende del caso específico, pero en general, las **CTEs** son preferibles cuando se busca claridad y facilidad de mantenimiento.
