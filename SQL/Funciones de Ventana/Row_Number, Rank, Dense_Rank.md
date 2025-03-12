
### 1. **ROW_NUMBER()**

La función **ROW_NUMBER()** asigna un número único a cada fila en el conjunto de resultados. El número se asigna de acuerdo con el orden especificado en la consulta y siempre comienza desde 1.

#### Sintaxis:

```sql
ROW_NUMBER() OVER (ORDER BY columna)
```

#### Ejemplos:

- **ROW_NUMBER() básico**:

```sql
SELECT nombre, salario, ROW_NUMBER() OVER (ORDER BY salario DESC) AS ranking_salario
FROM Empleados;
```
Este ejemplo asigna un número de fila a cada empleado según su salario, de mayor a menor. El empleado con el salario más alto tendrá el número 1.

- **ROW_NUMBER() con partición**:

```sql
SELECT nombre, departamento_id, salario, 
       ROW_NUMBER() OVER (PARTITION BY departamento_id ORDER BY salario DESC) AS ranking_departamento
FROM Empleados;
```
Este ejemplo asigna un número de fila para cada empleado dentro de su departamento, ordenado por salario de mayor a menor. Los empleados de diferentes departamentos tendrán números de fila separados.

- **ROW_NUMBER() para eliminar duplicados**:

```sql
WITH Empleados_ordenados AS (
  SELECT nombre, salario, ROW_NUMBER() OVER (PARTITION BY nombre ORDER BY salario DESC) AS rn
  FROM Empleados
)
SELECT nombre, salario
FROM Empleados_ordenados
WHERE rn = 1;
```
Este ejemplo usa **ROW_NUMBER()** para obtener el salario más alto de cada empleado (eliminando duplicados de empleados con el mismo nombre).

---

### 2. **RANK()**

La función **RANK()** asigna un número de ranking a cada fila, pero con un detalle: si dos filas tienen el mismo valor en el campo de orden, ambas recibirán el mismo rango, y se "saltará" el siguiente número de ranking.

#### Sintaxis:

```sql
RANK() OVER (ORDER BY columna)
```

#### Ejemplos:

- **RANK() básico**:

```sql
SELECT nombre, salario, RANK() OVER (ORDER BY salario DESC) AS ranking_salario
FROM Empleados;
```
Este ejemplo asigna un ranking a los empleados basado en su salario. Si dos empleados tienen el mismo salario, ambos recibirán el mismo rango, pero el siguiente empleado será asignado con el siguiente número de rango disponible.

- **RANK() con partición**:

```sql
SELECT nombre, departamento_id, salario, 
       RANK() OVER (PARTITION BY departamento_id ORDER BY salario DESC) AS ranking_departamento
FROM Empleados;
```
Aquí, se asigna un ranking de salario dentro de cada departamento. Los empleados con el mismo salario recibirán el mismo rango dentro de su departamento.

- **RANK() para encontrar los mejores salarios**:

```sql
SELECT nombre, salario, RANK() OVER (ORDER BY salario DESC) AS ranking_salario
FROM Empleados
WHERE RANK() OVER (ORDER BY salario DESC) <= 3;
```
Este ejemplo selecciona los tres empleados con los salarios más altos. Usamos **RANK()** para obtener los tres primeros, incluso si hay empates en los salarios.

---

### 3. **DENSE_RANK()**

La función **DENSE_RANK()** es similar a **RANK()**, pero con una diferencia clave: no "salta" números en caso de empate. Si dos filas tienen el mismo valor, recibirán el mismo rango, pero el siguiente valor no se saltará.

#### Sintaxis:

```sql
DENSE_RANK() OVER (ORDER BY columna)
```

#### Ejemplos:

- **DENSE_RANK() básico**:

```sql
SELECT nombre, salario, DENSE_RANK() OVER (ORDER BY salario DESC) AS ranking_salario
FROM Empleados;
```
Este ejemplo asigna un ranking sin saltarse ningún número, incluso cuando hay empates. Si dos empleados tienen el mismo salario, ambos recibirán el mismo rango, pero el siguiente empleado recibirá el siguiente rango consecutivo.

- **DENSE_RANK() con partición**:

```sql
SELECT nombre, departamento_id, salario, 
       DENSE_RANK() OVER (PARTITION BY departamento_id ORDER BY salario DESC) AS ranking_departamento
FROM Empleados;
```
Aquí se calcula el ranking de salario por departamento sin saltarse números en caso de empate. El salario más alto de cada departamento recibe el primer lugar, el siguiente salario diferente el segundo, y así sucesivamente.

- **DENSE_RANK() para los mejores salarios sin saltos**:

```sql
SELECT nombre, salario, DENSE_RANK() OVER (ORDER BY salario DESC) AS ranking_salario
FROM Empleados
WHERE DENSE_RANK() OVER (ORDER BY salario DESC) <= 3;
```
Este ejemplo selecciona a los tres empleados con los salarios más altos, sin dejar huecos en los números de ranking, incluso si hay empates.

---

### Resumen

- **ROW_NUMBER()**: Asigna un número único a cada fila, empezando desde 1, sin importar los valores duplicados.
- **RANK()**: Asigna un número de ranking a cada fila, pero en caso de empate, se asigna el mismo número y se salta el siguiente.
- **DENSE_RANK()**: Similar a **RANK()**, pero no salta números en caso de empate; todos los valores duplicados reciben el mismo rango y el siguiente valor recibe el siguiente número consecutivo.

Las funciones **ROW_NUMBER()**, **RANK()** y **DENSE_RANK()** son muy útiles para clasificar y ordenar datos de manera flexible, dependiendo de cómo quieras manejar los empates.
