
Las **funciones de ventana (window functions)** permiten realizar cálculos avanzados en un conjunto de filas relacionadas con la fila actual, sin necesidad de agrupar los datos. Estas funciones son muy útiles para realizar cálculos como **promedios móviles**, **ranking** o **comparaciones de filas adyacentes**.

## Funciones de Ventana (Window Functions)

Una **función de ventana** realiza cálculos a través de un conjunto de filas relacionadas (conocido como **ventana**), pero sin agruparlas. Esto permite que cada fila conserve su valor individual mientras se calcula la función sobre un conjunto de datos.

Las funciones de ventana se usan con la cláusula **OVER()**, que define cómo se divide el conjunto de datos en particiones y cómo se ordenan las filas dentro de cada partición.

### Ejemplo básico de función de ventana:

```sql
SELECT employee_id, salary,
       AVG(salary) OVER () AS avg_salary
FROM employees;
```

Este ejemplo calcula el salario promedio de todos los empleados sin agrupar los datos, utilizando la función de ventana `AVG()`.

## Funciones Avanzadas Comunes

### 1. **LAG()**

La función **LAG()** devuelve el valor de una fila anterior dentro de la misma partición. Se usa para comparar el valor de la fila actual con una fila previa. Si no existe una fila anterior, se puede devolver un valor `NULL` o un valor por defecto.

#### Sintaxis:
```sql
LAG(expression, offset, default) OVER (PARTITION BY partition_column ORDER BY order_column)
```

- **expression**: La columna o expresión de la que quieres obtener el valor.
- **offset**: El número de filas hacia atrás que se quiere mirar (por defecto es 1).
- **default**: Valor por defecto si no hay fila previa (opcional).
- **PARTITION BY**: Divide las filas en particiones.
- **ORDER BY**: Define el orden de las filas dentro de cada partición.

#### Ejemplo:
```sql
SELECT order_id, order_date, 
       LAG(order_date) OVER (ORDER BY order_date) AS previous_order_date
FROM orders;
```

En este ejemplo, la consulta devuelve la fecha del pedido anterior (`previous_order_date`) para cada pedido, ordenado por la fecha de pedido.

### 2. **LEAD()**

La función **LEAD()** es similar a **LAG()**, pero en lugar de mirar hacia atrás, mira hacia adelante en las filas dentro de la misma partición.

#### Sintaxis:
```sql
LEAD(expression, offset, default) OVER (PARTITION BY partition_column ORDER BY order_column)
```

- **expression**: La columna o expresión de la que deseas obtener el valor de la siguiente fila.
- **offset**: El número de filas hacia adelante que deseas mirar (por defecto es 1).
- **default**: Valor por defecto si no existe una fila posterior (opcional).
- **PARTITION BY**: Divide las filas en particiones.
- **ORDER BY**: Define el orden de las filas dentro de cada partición.

#### Ejemplo:
```sql
SELECT order_id, order_date,
       LEAD(order_date) OVER (ORDER BY order_date) AS next_order_date
FROM orders;
```

Este ejemplo devuelve la fecha del próximo pedido (`next_order_date`) para cada pedido.

### 3. **RANK()**

La función **RANK()** asigna un número de clasificación único a cada fila dentro de una partición, según un orden especificado. Si hay empates (es decir, filas con el mismo valor de clasificación), las filas empatadas reciben el mismo rango, pero se omiten rangos subsecuentes.

#### Sintaxis:
```sql
RANK() OVER (PARTITION BY partition_column ORDER BY order_column)
```

- **PARTITION BY**: Divide las filas en particiones.
- **ORDER BY**: Define el orden de las filas dentro de cada partición.

#### Ejemplo:
```sql
SELECT employee_id, salary,
       RANK() OVER (ORDER BY salary DESC) AS rank
FROM employees;
```

En este ejemplo, los empleados se ordenan por salario de mayor a menor, y a cada uno se le asigna un rango. Si varios empleados tienen el mismo salario, recibirán el mismo rango, pero el siguiente empleado recibirá un rango incrementado.

### 4. **DENSE_RANK()**

**DENSE_RANK()** es similar a **RANK()**, pero no omite rangos en caso de empate. Es decir, si hay empates, el siguiente valor no salta al siguiente número disponible, sino que continúa de forma secuencial.

#### Ejemplo:
```sql
SELECT employee_id, salary,
       DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_rank
FROM employees;
```

Aquí, los empleados con el mismo salario reciben el mismo rango, pero el siguiente salario diferente recibe el siguiente rango secuencial.

## Otras Funciones de Ventana Comunes

- **NTILE(n)**: Divide las filas en n grupos de tamaño aproximadamente igual y asigna un número a cada grupo.
- **ROW_NUMBER()**: Asigna un número de fila único y secuencial a cada fila en la partición especificada.

### Ejemplo con `ROW_NUMBER()`:
```sql
SELECT employee_id, salary,
       ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_number
FROM employees;
```

Este ejemplo asigna un número secuencial a cada fila, basado en el orden de salario.

## Conclusión

Las funciones de ventana en SQL permiten realizar cálculos avanzados sin necesidad de agrupar los datos, lo que ofrece gran flexibilidad. Funciones como **LAG()**, **LEAD()**, **RANK()** y **DENSE_RANK()** son especialmente útiles para:

- Comparar valores entre filas adyacentes.
- Asignar rangos a los datos.
- Realizar cálculos agregados avanzados mientras se conserva la granularidad de los datos.

Estas funciones son fundamentales para análisis de series temporales, análisis comparativos y clasificación de datos.
