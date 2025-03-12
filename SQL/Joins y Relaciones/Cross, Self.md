
### 5. **CROSS JOIN**

El **CROSS JOIN** devuelve el producto cartesiano de las dos tablas, es decir, combina todas las filas de la primera tabla con todas las filas de la segunda tabla. Esto puede generar un número muy grande de resultados, especialmente si las tablas son grandes.

#### Ejemplos:

- **CROSS JOIN básico:**

```sql
SELECT Empleados.nombre, Proyectos.nombre
FROM Empleados
CROSS JOIN Proyectos;
```
Este ejemplo devuelve todas las combinaciones posibles entre empleados y proyectos. Si hay 5 empleados y 3 proyectos, el resultado será de 15 filas.

- **CROSS JOIN con condiciones adicionales:**

```sql
SELECT Clientes.nombre, Productos.nombre
FROM Clientes
CROSS JOIN Productos
WHERE Productos.precio > 100;
```
Este ejemplo devuelve todas las combinaciones posibles entre clientes y productos cuyo precio es mayor a 100.

- **CROSS JOIN con más de dos tablas:**

```sql
SELECT Empleados.nombre, Proyectos.nombre, Departamentos.nombre
FROM Empleados
CROSS JOIN Proyectos
CROSS JOIN Departamentos;
```
Este ejemplo devuelve todas las combinaciones posibles entre empleados, proyectos y departamentos.

---

### 6. **Self JOIN**

El **Self JOIN** es un join de una tabla consigo misma. Se usa cuando necesitas comparar filas dentro de la misma tabla. Al hacer un self join, es necesario usar alias para diferenciar las dos instancias de la misma tabla.

#### Ejemplos:

- **Self JOIN para comparar registros en la misma tabla:**

```sql
SELECT E1.nombre AS empleado, E2.nombre AS supervisor
FROM Empleados E1
LEFT JOIN Empleados E2 ON E1.supervisor_id = E2.id;
```
Este ejemplo muestra los empleados junto con el nombre de su supervisor. Aquí, se usa la misma tabla **Empleados** dos veces: una para los empleados (`E1`) y otra para los supervisores (`E2`).

- **Self JOIN para encontrar relaciones jerárquicas:**

```sql
SELECT E1.nombre AS empleado, E2.nombre AS jefe
FROM Empleados E1
INNER JOIN Empleados E2 ON E1.jefe_id = E2.id;
```
Este ejemplo obtiene los empleados y sus respectivos jefes en una estructura jerárquica dentro de la misma tabla de empleados.

- **Self JOIN para encontrar empleados con el mismo salario:**

```sql
SELECT E1.nombre AS empleado1, E2.nombre AS empleado2
FROM Empleados E1
INNER JOIN Empleados E2 ON E1.salario = E2.salario
WHERE E1.id != E2.id;
```
Este ejemplo encuentra todos los pares de empleados que tienen el mismo salario, pero excluye el emparejamiento de un empleado consigo mismo.

---

### Resumen

- **CROSS JOIN**: Devuelve el producto cartesiano de dos tablas, generando todas las combinaciones posibles entre las filas de ambas.
- **Self JOIN**: Se utiliza para hacer un join de una tabla consigo misma, utilizando alias para distinguir entre las dos instancias de la misma tabla.

El **CROSS JOIN** es útil en casos específicos como análisis combinatorios, mientras que el **Self JOIN** es muy útil cuando se trabaja con datos jerárquicos o relaciones dentro de una misma tabla.
