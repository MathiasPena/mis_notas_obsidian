
### 4. **IS NULL**

La cláusula **IS NULL** se utiliza para verificar si un valor es **NULL**, lo cual significa que no tiene valor asignado. Es útil cuando quieres encontrar registros con valores ausentes.

#### Ejemplos:

- **Filtrar registros con valor NULL:**

```sql
SELECT nombre, email
FROM Clientes
WHERE email IS NULL;
```
Este ejemplo selecciona a todos los clientes que no tienen un email registrado (es decir, cuyo campo `email` es `NULL`).

- **Filtrar registros sin valor en una fecha de nacimiento:**

```sql
SELECT nombre, fecha_nacimiento
FROM Empleados
WHERE fecha_nacimiento IS NULL;
```
Filtra a los empleados que no tienen fecha de nacimiento registrada.

- **Filtrar registros con valores no nulos usando IS NOT NULL:**

```sql
SELECT nombre, telefono
FROM Clientes
WHERE telefono IS NOT NULL;
```
Este ejemplo selecciona todos los clientes que tienen un teléfono registrado (es decir, su campo `telefono` no es `NULL`).

---

### 5. **COALESCE()**

La función **COALESCE()** devuelve el primer valor no nulo de una lista de expresiones. Es muy útil cuando quieres reemplazar valores **NULL** por un valor predeterminado.

#### Sintaxis:

```sql
SELECT COALESCE(columna, valor_predeterminado)
FROM tabla;
```

#### Ejemplos:

- **Reemplazar valores NULL con un valor predeterminado:**

```sql
SELECT nombre, COALESCE(email, 'Email no disponible') AS email
FROM Clientes;
```
Este ejemplo selecciona el nombre de los clientes y reemplaza los valores `NULL` del campo `email` por la cadena "Email no disponible".

- **Usar COALESCE con múltiples columnas:**

```sql
SELECT nombre, COALESCE(telefono, email, 'Sin contacto') AS contacto
FROM Clientes;
```
Este ejemplo selecciona el nombre de los clientes y, si el `telefono` es `NULL`, intenta usar el `email`. Si ambos son `NULL`, muestra "Sin contacto".

- **Aplicación en una lista de valores:**

```sql
SELECT nombre, COALESCE(edad, 18) AS edad
FROM Estudiantes;
```
Este ejemplo selecciona los nombres de los estudiantes y reemplaza los valores `NULL` en la columna `edad` con 18.

- **Usar COALESCE con valores nulos y no nulos:**

```sql
SELECT producto, COALESCE(precio, 0) AS precio
FROM Productos;
```
Este ejemplo devuelve el precio de los productos, pero si el valor de `precio` es `NULL`, lo reemplaza por 0.

---

### Resumen

- **IS NULL / IS NOT NULL**: Filtra registros que tienen valores nulos o no nulos en una columna.
- **COALESCE()**: Devuelve el primer valor no nulo de una lista de expresiones, útil para manejar valores nulos y reemplazarlos por un valor predeterminado.
