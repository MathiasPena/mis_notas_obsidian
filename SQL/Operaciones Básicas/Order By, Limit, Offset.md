# Operaciones Básicas: ORDER BY, LIMIT, OFFSET

Las cláusulas **ORDER BY**, **LIMIT** y **OFFSET** son muy útiles para controlar el orden y la cantidad de los resultados devueltos por una consulta SQL. Son fundamentales cuando deseas organizar los datos de una manera específica o cuando solo necesitas una parte de los resultados.

## ORDER BY

La cláusula **ORDER BY** se utiliza para ordenar los resultados de una consulta según una o varias columnas. Puedes ordenar los resultados en orden ascendente (`ASC`) o descendente (`DESC`).

### Sintaxis Básica:

```sql
SELECT columna1, columna2, ...
FROM tabla
ORDER BY columna1 [ASC|DESC], columna2 [ASC|DESC], ...;
```

### Ejemplo:

```sql
SELECT nombre, email
FROM Clientes
ORDER BY nombre ASC;
```

Este ejemplo ordena los resultados por el `nombre` de los clientes en orden ascendente (alfabético).

### Ordenar por múltiples columnas:

```sql
SELECT nombre, email
FROM Clientes
ORDER BY nombre ASC, email DESC;
```

En este caso, primero se ordenan los resultados por `nombre` en orden ascendente, y luego, en caso de que haya duplicados en `nombre`, se ordenan por `email` en orden descendente.

## LIMIT

La cláusula **LIMIT** se usa para restringir la cantidad de resultados que devuelve una consulta. Es útil cuando solo deseas obtener una parte de los resultados, como los primeros 10 registros.

### Sintaxis Básica:

```sql
SELECT columna1, columna2, ...
FROM tabla
LIMIT número_de_resultados;
```

### Ejemplo:

```sql
SELECT nombre, email
FROM Clientes
LIMIT 5;
```

Este ejemplo devuelve solo los primeros 5 registros de la tabla `Clientes`.

### LIMIT y ORDER BY:

Cuando usas **ORDER BY** junto con **LIMIT**, puedes obtener una lista ordenada y luego limitar la cantidad de resultados.

```sql
SELECT nombre, email
FROM Clientes
ORDER BY nombre ASC
LIMIT 3;
```

Este ejemplo devuelve los primeros 3 clientes, ordenados alfabéticamente por `nombre`.

## OFFSET

La cláusula **OFFSET** se usa para saltar un número determinado de registros en los resultados. Es comúnmente utilizada junto con **LIMIT** para paginar los resultados.

### Sintaxis Básica:

```sql
SELECT columna1, columna2, ...
FROM tabla
LIMIT número_de_resultados OFFSET número_de_registros_a_saltar;
```

### Ejemplo:

```sql
SELECT nombre, email
FROM Clientes
LIMIT 5 OFFSET 5;
```

Este ejemplo devuelve los 5 registros siguientes de la tabla `Clientes`, saltando los primeros 5.

### Ejemplo de paginación:

Para realizar paginación en una consulta, puedes usar **LIMIT** y **OFFSET** en combinación. Por ejemplo, para obtener la segunda página de 5 resultados:

```sql
SELECT nombre, email
FROM Clientes
LIMIT 5 OFFSET 5;
```

Esto devolverá los resultados de la segunda "página" de 5 registros.

## Resumen de ORDER BY, LIMIT, OFFSET

- **ORDER BY**: Ordena los resultados de una consulta según las columnas especificadas.
- **LIMIT**: Restringe la cantidad de resultados devueltos por una consulta.
- **OFFSET**: Omite una cantidad determinada de registros al principio de los resultados.