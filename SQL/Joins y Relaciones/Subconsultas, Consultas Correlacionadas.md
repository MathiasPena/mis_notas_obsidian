## Joins y Relaciones: Subconsultas y Consultas Correlacionadas

### 7. **Subconsultas**

Una **subconsulta** es una consulta dentro de otra consulta. Las subconsultas pueden aparecer en las cláusulas **SELECT**, **FROM**, **WHERE**, y **HAVING**. Existen dos tipos de subconsultas: **subconsultas escalar** (devuelven un solo valor) y **subconsultas de conjunto** (devuelven varios valores).

#### Ejemplos de Subconsultas:

- **Subconsulta en la cláusula WHERE:**

```sql
SELECT nombre, salario
FROM Empleados
WHERE salario > (SELECT AVG(salario) FROM Empleados);
```
Este ejemplo selecciona los empleados cuyo salario es mayor que el salario promedio de todos los empleados.

- **Subconsulta en la cláusula SELECT:**

```sql
SELECT nombre, 
       (SELECT COUNT(*) FROM Pedidos WHERE Pedidos.id_cliente = Clientes.id_cliente) AS cantidad_pedidos
FROM Clientes;
```
Este ejemplo muestra los clientes y la cantidad de pedidos que tiene cada uno. La subconsulta cuenta los pedidos de cada cliente.

- **Subconsulta en la cláusula FROM:**

```sql
SELECT departamento_id, AVG(salario) 
FROM (SELECT departamento_id, salario FROM Empleados WHERE salario > 3000) AS empleados_alto_salario
GROUP BY departamento_id;
```
En este ejemplo, la subconsulta en el **FROM** filtra a los empleados con un salario mayor a 3000 y luego se calcula el salario promedio por departamento.

- **Subconsulta con IN:**

```sql
SELECT nombre
FROM Empleados
WHERE departamento_id IN (SELECT id FROM Departamentos WHERE nombre = 'Ventas');
```
Este ejemplo selecciona los empleados que trabajan en el departamento de "Ventas". La subconsulta obtiene el id de dicho departamento.

---

### 8. **Consultas Correlacionadas**

Una **consulta correlacionada** es una subconsulta que depende de los valores de la fila que se está evaluando en la consulta externa. La subconsulta se ejecuta para cada fila procesada en la consulta externa.

#### Ejemplos de Consultas Correlacionadas:

- **Subconsulta correlacionada en WHERE:**

```sql
SELECT nombre, salario
FROM Empleados E1
WHERE salario > (SELECT AVG(salario) 
                 FROM Empleados E2 
                 WHERE E1.departamento_id = E2.departamento_id);
```
Este ejemplo muestra los empleados cuyo salario es mayor que el salario promedio de su mismo departamento. La subconsulta depende de la fila actual de la consulta externa (por eso es correlacionada).

- **Subconsulta correlacionada con EXISTS:**

```sql
SELECT nombre
FROM Empleados E1
WHERE EXISTS (SELECT 1 FROM Pedidos P WHERE P.id_cliente = E1.id_cliente AND P.fecha > '2023-01-01');
```
Este ejemplo muestra los empleados que tienen al menos un pedido después del 1 de enero de 2023. La subconsulta comprueba la existencia de pedidos para cada empleado.

- **Subconsulta correlacionada en SELECT:**

```sql
SELECT nombre, 
       (SELECT MAX(salario) 
        FROM Empleados E2 
        WHERE E1.departamento_id = E2.departamento_id) AS salario_maximo
FROM Empleados E1;
```
Este ejemplo muestra los empleados y el salario máximo dentro de su departamento. La subconsulta obtiene el salario máximo de cada departamento, y se evalúa para cada fila de la consulta externa.

---

### Resumen

- **Subconsultas**: Son consultas dentro de otras consultas y pueden estar en las cláusulas **WHERE**, **FROM**, **SELECT**, y **HAVING**. Pueden ser escalar o de conjunto.
- **Consultas Correlacionadas**: Son subconsultas que dependen de la fila de la consulta externa. Se ejecutan para cada fila procesada en la consulta externa.

Las **subconsultas** son útiles para realizar consultas complejas donde necesitas comparar o filtrar basándote en valores agregados o de otras tablas. Las **consultas correlacionadas** son potentes cuando necesitas realizar operaciones que dependan de cada fila en la consulta principal.
