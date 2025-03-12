
## Filtros y Condiciones (WHERE, LIKE, BETWEEN, IN, IS NULL)

En SQL, las condiciones de filtro son esenciales para extraer datos específicos de una base de datos. Se utilizan en la cláusula **`WHERE`** para limitar los resultados de una consulta. Existen varias formas de filtrar datos utilizando operadores como **`LIKE`**, **`BETWEEN`**, **`IN`**, y **`IS NULL`**. A continuación, se explican cada uno de estos operadores y su uso en SQL.

## **1. WHERE** - Filtrar por condiciones

La cláusula **`WHERE`** se utiliza para especificar las condiciones que deben cumplirse para que las filas sean incluidas en los resultados de la consulta. Puedes usar operadores de comparación (como `=`, `<`, `>`, `!=`, etc.) para establecer las condiciones.

### Sintaxis básica:
```sql
SELECT columna1, columna2
FROM tabla
WHERE condición;
```

### Ejemplo:
```sql
SELECT nombre, salario
FROM empleados
WHERE salario > 50000;
```
Este ejemplo devuelve los **nombres** y **salarios** de los empleados cuyo salario es mayor a 50,000.

## **2. LIKE** - Búsqueda de patrones

El operador **`LIKE`** se utiliza para buscar patrones dentro de los valores de una columna de tipo texto. Se usa en combinación con los caracteres comodín **`%`** (que representa cualquier número de caracteres) y **`_`** (que representa un solo carácter).

### Sintaxis básica:
```sql
SELECT columna1
FROM tabla
WHERE columna1 LIKE 'patrón';
```

### Ejemplo:
```sql
SELECT nombre
FROM empleados
WHERE nombre LIKE 'J%';
```
Este ejemplo devuelve los **nombres** de los empleados que comienzan con la letra "J".

## **3. BETWEEN** - Rango de valores

El operador **`BETWEEN`** se utiliza para filtrar los resultados dentro de un rango determinado. Puede aplicarse a números, fechas y otros tipos de datos.

### Sintaxis básica:
```sql
SELECT columna1
FROM tabla
WHERE columna1 BETWEEN valor_inicial AND valor_final;
```

### Ejemplo:
```sql
SELECT nombre, salario
FROM empleados
WHERE salario BETWEEN 40000 AND 60000;
```
Este ejemplo devuelve los **nombres** y **salarios** de los empleados cuyo salario está entre 40,000 y 60,000 (inclusive).

## **4. IN** - Conjunto de valores

El operador **`IN`** se utiliza para filtrar los resultados de una consulta con base en un conjunto de valores específicos. Es más eficiente que usar múltiples condiciones con **`OR`**.

### Sintaxis básica:
```sql
SELECT columna1
FROM tabla
WHERE columna1 IN (valor1, valor2, valor3, ...);
```

### Ejemplo:
```sql
SELECT nombre
FROM empleados
WHERE departamento IN ('Ventas', 'Marketing');
```
Este ejemplo devuelve los **nombres** de los empleados que pertenecen a los departamentos de **Ventas** o **Marketing**.

## **5. IS NULL** - Verificar valores nulos

El operador **`IS NULL`** se utiliza para verificar si una columna tiene valores **NULL**. Es útil cuando se quiere encontrar filas que no tienen datos en ciertas columnas.

### Sintaxis básica:
```sql
SELECT columna1
FROM tabla
WHERE columna1 IS NULL;
```

### Ejemplo:
```sql
SELECT nombre
FROM empleados
WHERE fecha_terminacion IS NULL;
```
Este ejemplo devuelve los **nombres** de los empleados cuya fecha de terminación es **NULL** (es decir, que no tienen fecha de terminación registrada).

## **Combinando Condiciones**

Es posible combinar múltiples condiciones utilizando los operadores **`AND`** y **`OR`** para hacer filtros más complejos.

### Ejemplo con **`AND`**:
```sql
SELECT nombre, salario
FROM empleados
WHERE salario > 50000 AND departamento = 'Ventas';
```
Este ejemplo devuelve los **nombres** y **salarios** de los empleados cuyo salario es mayor a 50,000 y trabajan en el departamento de **Ventas**.

### Ejemplo con **`OR`**:
```sql
SELECT nombre
FROM empleados
WHERE departamento = 'Ventas' OR departamento = 'Marketing';
```
Este ejemplo devuelve los **nombres** de los empleados que trabajan en los departamentos de **Ventas** o **Marketing**.

## **Conclusión**

El uso de filtros y condiciones en SQL es fundamental para realizar consultas eficientes y obtener resultados específicos. Algunos de los operadores más comunes son:

- **`WHERE`**: para filtrar según condiciones.
- **`LIKE`**: para buscar patrones en cadenas de texto.
- **`BETWEEN`**: para filtrar valores dentro de un rango.
- **`IN`**: para filtrar valores dentro de un conjunto.
- **`IS NULL`**: para verificar si un valor es **NULL**.

Estos operadores permiten crear consultas más poderosas y adaptadas a las necesidades de los datos que estamos buscando.
