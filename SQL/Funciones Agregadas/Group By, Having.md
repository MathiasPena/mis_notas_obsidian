
### 6. **GROUP BY**

La cláusula **GROUP BY** se utiliza para agrupar los resultados de una consulta en función de una o más columnas. Se suele usar en conjunto con funciones agregadas como **COUNT()**, **SUM()**, **AVG()**, **MIN()**, y **MAX()** para obtener estadísticas por grupos.

#### Ejemplos:

- **Agrupar por una columna:**

```sql
SELECT departamento_id, COUNT(*) AS cantidad_empleados
FROM Empleados
GROUP BY departamento_id;
```
Este ejemplo cuenta el número de empleados por cada departamento.

- **Agrupar por varias columnas:**

```sql
SELECT ciudad, estado, AVG(salario) AS salario_promedio
FROM Empleados
GROUP BY ciudad, estado;
```
Este ejemplo calcula el salario promedio de los empleados agrupados por ciudad y estado.

- **Agrupar y ordenar los resultados:**

```sql
SELECT categoria, SUM(ventas) AS total_ventas
FROM Productos
GROUP BY categoria
ORDER BY total_ventas DESC;
```
Este ejemplo agrupa los productos por categoría y luego ordena los resultados por el total de ventas, de mayor a menor.

- **Agrupar por fecha:**

```sql
SELECT YEAR(fecha_venta) AS año, SUM(monto) AS total_ventas
FROM Ventas
GROUP BY YEAR(fecha_venta);
```
Este ejemplo agrupa las ventas por año y calcula el total de ventas por cada uno.

---

### 7. **HAVING**

La cláusula **HAVING** se usa para filtrar los resultados después de aplicar **GROUP BY**. A diferencia de **WHERE**, que filtra los registros antes de la agrupación, **HAVING** permite aplicar condiciones a los grupos resultantes.

#### Ejemplos:

- **Filtrar grupos con una condición agregada:**

```sql
SELECT departamento_id, AVG(salario) AS salario_promedio
FROM Empleados
GROUP BY departamento_id
HAVING AVG(salario) > 3000;
```
Este ejemplo selecciona los departamentos cuyo salario promedio es mayor a 3000.

- **Filtrar por el número de registros en cada grupo:**

```sql
SELECT ciudad, COUNT(*) AS cantidad_clientes
FROM Clientes
GROUP BY ciudad
HAVING COUNT(*) > 10;
```
Este ejemplo selecciona las ciudades con más de 10 clientes registrados.

- **Usar HAVING con múltiples condiciones:**

```sql
SELECT categoria, SUM(ventas) AS total_ventas
FROM Productos
GROUP BY categoria
HAVING SUM(ventas) > 1000 AND COUNT(*) > 5;
```
Este ejemplo selecciona las categorías de productos cuya suma de ventas es mayor a 1000 y que tienen más de 5 productos vendidos.

- **Filtrar usando una condición en un campo agregado:**

```sql
SELECT departamento_id, MAX(fecha_ingreso) AS ultima_fecha_ingreso
FROM Empleados
GROUP BY departamento_id
HAVING MAX(fecha_ingreso) > '2023-01-01';
```
Este ejemplo selecciona los departamentos cuyo último empleado ingresó después del 1 de enero de 2023.

---

### Resumen

- **GROUP BY**: Agrupa los resultados de la consulta según una o más columnas, permitiendo realizar funciones agregadas sobre esos grupos.
- **HAVING**: Filtra los resultados de la consulta después de agruparlos, basándose en condiciones aplicadas a las funciones agregadas.
