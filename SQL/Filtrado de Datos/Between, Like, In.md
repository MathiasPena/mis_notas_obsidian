
### 1. **BETWEEN**

El operador **BETWEEN** se utiliza para filtrar registros que se encuentran dentro de un rango de valores. Este operador es inclusivo, es decir, incluye tanto el valor inferior como el valor superior del rango. Puedes usarlo con números, fechas o incluso cadenas de texto.

#### Ejemplos:

- **Rango de fechas:**

```sql
SELECT nombre, fecha_nacimiento
FROM Empleados
WHERE fecha_nacimiento BETWEEN '1980-01-01' AND '1990-12-31';
```
Este ejemplo selecciona a los empleados nacidos entre el 1 de enero de 1980 y el 31 de diciembre de 1990.

- **Rango de números:**

```sql
SELECT producto, precio
FROM Productos
WHERE precio BETWEEN 100 AND 500;
```
Filtra los productos cuyo precio está entre 100 y 500.

- **Rango alfabético:**

```sql
SELECT nombre
FROM Clientes
WHERE nombre BETWEEN 'Ana' AND 'Lucas';
```
Selecciona los clientes cuyos nombres están entre "Ana" y "Lucas" en orden alfabético.

- **Rango con valores decimales:**

```sql
SELECT producto, cantidad
FROM Inventario
WHERE cantidad BETWEEN 10.5 AND 50.5;
```
Selecciona los productos cuya cantidad en inventario está entre 10.5 y 50.5.

---

### 2. **LIKE**

El operador **LIKE** se usa para buscar patrones en cadenas de texto. Utiliza los comodines `%` (para cualquier número de caracteres) y `_` (para un solo carácter).

#### Ejemplos:

- **Búsqueda que comienza con un patrón:**

```sql
SELECT nombre, email
FROM Clientes
WHERE nombre LIKE 'Mar%';
```
Este ejemplo selecciona todos los clientes cuyo nombre comienza con "Mar" (ej. "Maria", "Martín").

- **Búsqueda que termina con un patrón:**

```sql
SELECT nombre, email
FROM Clientes
WHERE nombre LIKE '%son';
```
Selecciona a los clientes cuyo nombre termina en "son" (ej. "Anderson", "Jackson").

- **Búsqueda que contiene un patrón:**

```sql
SELECT nombre, email
FROM Clientes
WHERE nombre LIKE '%van%';
```
Este ejemplo selecciona a los clientes cuyo nombre contiene "van" en cualquier parte (ej. "Ivan", "Javier").

- **Uso del comodín `_` (un solo carácter):**

```sql
SELECT nombre
FROM Clientes
WHERE nombre LIKE '_a%';
```
Este ejemplo selecciona todos los clientes cuyos nombres tienen "a" en la segunda posición (ej. "Carlos", "Marta").

---

### 3. **IN**

El operador **IN** se utiliza para filtrar registros que coinciden con un conjunto de valores específicos. Es más eficiente que usar múltiples condiciones **OR**.

#### Ejemplos:

- **Filtrar por varios valores:**

```sql
SELECT nombre, email
FROM Clientes
WHERE id_cliente IN (1, 3, 5, 7);
```
Este ejemplo selecciona los clientes con los IDs 1, 3, 5 y 7.

- **Filtrar por varios valores de texto:**

```sql
SELECT nombre, ciudad
FROM Proveedores
WHERE ciudad IN ('Montevideo', 'Buenos Aires', 'Santiago');
```
Selecciona los proveedores ubicados en Montevideo, Buenos Aires o Santiago.

- **Filtrar por un conjunto de fechas:**

```sql
SELECT evento, fecha
FROM Eventos
WHERE fecha IN ('2025-03-01', '2025-05-10', '2025-07-21');
```
Este ejemplo selecciona eventos que ocurren en fechas específicas.

- **Uso de **NOT IN** para excluir valores:**

```sql
SELECT nombre
FROM Empleados
WHERE departamento_id NOT IN (2, 3);
```
Este ejemplo selecciona empleados que no pertenecen a los departamentos con ID 2 y 3.

---

### Resumen

- **BETWEEN**: Filtra registros dentro de un rango de valores (inclusive).
- **LIKE**: Filtra registros que coinciden con un patrón de texto.
- **IN**: Filtra registros que coinciden con cualquiera de los valores de un conjunto.
