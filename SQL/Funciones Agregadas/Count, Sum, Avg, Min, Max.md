
### 1. **COUNT()**

La función **COUNT()** se utiliza para contar el número de registros en una columna o en toda una tabla. Es comúnmente utilizada para contar filas que cumplen con una condición.

#### Ejemplos:

- **Contar el número de registros en una tabla:**

```sql
SELECT COUNT(*) AS total_empleados
FROM Empleados;
```
Este ejemplo cuenta todos los empleados en la tabla `Empleados`.

- **Contar registros con una condición:**

```sql
SELECT COUNT(*) AS empleados_activos
FROM Empleados
WHERE estado = 'Activo';
```
Cuenta cuántos empleados tienen el estado "Activo".

- **Contar registros con una condición en una columna específica:**

```sql
SELECT COUNT(email) AS total_con_email
FROM Clientes
WHERE email IS NOT NULL;
```
Cuenta cuántos clientes tienen un email registrado (es decir, no es `NULL`).

---

### 2. **SUM()**

La función **SUM()** devuelve la suma total de los valores numéricos de una columna. Se utiliza comúnmente con valores monetarios, cantidades, etc.

#### Ejemplos:

- **Sumar una columna de números:**

```sql
SELECT SUM(ventas) AS total_ventas
FROM Ventas;
```
Este ejemplo devuelve el total de ventas realizadas.

- **Sumar con condición:**

```sql
SELECT SUM(monto) AS total_facturado
FROM Facturas
WHERE estado = 'Pagada';
```
Este ejemplo calcula el total facturado por las facturas que ya han sido pagadas.

- **Sumar con rangos de fechas:**

```sql
SELECT SUM(monto) AS ventas_marzo
FROM Ventas
WHERE fecha BETWEEN '2025-03-01' AND '2025-03-31';
```
Este ejemplo devuelve el total de ventas realizadas durante el mes de marzo de 2025.

---

### 3. **AVG()**

La función **AVG()** devuelve el promedio de los valores numéricos en una columna. Es útil para calcular promedios, como el promedio de edades, salarios, etc.

#### Ejemplos:

- **Calcular el promedio de una columna:**

```sql
SELECT AVG(salario) AS salario_promedio
FROM Empleados;
```
Este ejemplo calcula el salario promedio de todos los empleados.

- **Calcular el promedio con una condición:**

```sql
SELECT AVG(calificacion) AS promedio_calificacion
FROM Estudiantes
WHERE curso = 'Matemáticas';
```
Este ejemplo calcula la calificación promedio de los estudiantes en el curso de Matemáticas.

- **Promedio de valores dentro de un rango de fechas:**

```sql
SELECT AVG(precio) AS precio_promedio
FROM Productos
WHERE fecha_venta BETWEEN '2025-01-01' AND '2025-12-31';
```
Este ejemplo calcula el precio promedio de los productos vendidos durante 2025.

---

### 4. **MIN()**

La función **MIN()** devuelve el valor mínimo de una columna. Es útil para encontrar el valor más bajo en una serie de datos, como el salario más bajo, la fecha más antigua, etc.

#### Ejemplos:

- **Encontrar el valor mínimo en una columna:**

```sql
SELECT MIN(salario) AS salario_minimo
FROM Empleados;
```
Este ejemplo devuelve el salario más bajo entre los empleados.

- **Encontrar el precio más bajo de un producto:**

```sql
SELECT MIN(precio) AS precio_minimo
FROM Productos;
```
Este ejemplo selecciona el precio más bajo entre todos los productos.

- **Encontrar la fecha más antigua:**

```sql
SELECT MIN(fecha_nacimiento) AS fecha_nacimiento_mas_antigua
FROM Empleados;
```
Este ejemplo selecciona la fecha de nacimiento más antigua de los empleados.

---

### 5. **MAX()**

La función **MAX()** devuelve el valor máximo de una columna. Es útil para encontrar el valor más alto en una serie de datos, como el salario más alto, la fecha más reciente, etc.

#### Ejemplos:

- **Encontrar el valor máximo en una columna:**

```sql
SELECT MAX(salario) AS salario_maximo
FROM Empleados;
```
Este ejemplo devuelve el salario más alto entre todos los empleados.

- **Encontrar el precio más alto de un producto:**

```sql
SELECT MAX(precio) AS precio_maximo
FROM Productos;
```
Este ejemplo selecciona el precio más alto entre todos los productos.

- **Encontrar la fecha más reciente:**

```sql
SELECT MAX(fecha_venta) AS fecha_venta_mas_reciente
FROM Ventas;
```
Este ejemplo devuelve la fecha más reciente en la que se registró una venta.

---

### Resumen

- **COUNT()**: Cuenta el número de registros.
- **SUM()**: Suma los valores numéricos.
- **AVG()**: Calcula el promedio de valores numéricos.
- **MIN()**: Encuentra el valor mínimo.
- **MAX()**: Encuentra el valor máximo.
