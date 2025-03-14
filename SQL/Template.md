# SQL Template para Trainee Data Engineer

## 1. **Fundamentos de SQL**
SQL (Structured Query Language) es el lenguaje utilizado para interactuar con bases de datos relacionales. Permite manipular y consultar datos almacenados en tablas.

### 1.1 **Bases de Datos Relacionales**
- **Base de datos**: Conjunto de datos organizados y almacenados en tablas.
- **Tabla**: Estructura que contiene datos organizados en filas y columnas.
- **Fila**: Una entrada de datos en la tabla.
- **Columna**: Un atributo de los datos que describe una propiedad específica.

### 1.2 **Claves**
- **Clave primaria (Primary Key)**: Identificador único de cada fila en una tabla.
- **Clave foránea (Foreign Key)**: Enlace entre dos tablas, donde una columna en una tabla referencia a la clave primaria de otra tabla.

---

## 2. **Operaciones Básicas en SQL**

### 2.1 **Consultas (SELECT)**
```sql
-- Seleccionar todas las columnas de una tabla
SELECT * FROM empleados;

-- Seleccionar columnas específicas
SELECT nombre, salario FROM empleados;
```

### 2.2 **Filtros (WHERE)**
```sql
-- Filtrar resultados con condiciones
SELECT * FROM empleados WHERE salario > 3000;
```

### 2.3 **Ordenar Resultados (ORDER BY)**
```sql
-- Ordenar de manera ascendente (ASC) o descendente (DESC)
SELECT * FROM empleados ORDER BY salario DESC;
```

### 2.4 **Limitar Resultados (LIMIT)**
```sql
-- Limitar el número de resultados
SELECT * FROM empleados LIMIT 5;
```

### 2.5 **Funciones de Agregación**
```sql
-- Contar registros
SELECT COUNT(*) FROM empleados;

-- Sumar valores
SELECT SUM(salario) FROM empleados;

-- Promedio
SELECT AVG(salario) FROM empleados;

-- Máximo
SELECT MAX(salario) FROM empleados;

-- Mínimo
SELECT MIN(salario) FROM empleados;
```

---

## 3. **Operaciones Avanzadas**

### 3.1 **Joins (Unir Tablas)**
- **INNER JOIN**: Retorna solo los registros que tienen coincidencias en ambas tablas.
```sql
SELECT empleados.nombre, departamentos.nombre
FROM empleados
INNER JOIN departamentos ON empleados.depto_id = departamentos.id;
```

- **LEFT JOIN**: Retorna todos los registros de la tabla izquierda, y los que coinciden de la tabla derecha.
```sql
SELECT empleados.nombre, departamentos.nombre
FROM empleados
LEFT JOIN departamentos ON empleados.depto_id = departamentos.id;
```

- **RIGHT JOIN**: Similar al LEFT JOIN, pero retorna todos los registros de la tabla derecha.
```sql
SELECT empleados.nombre, departamentos.nombre
FROM empleados
RIGHT JOIN departamentos ON empleados.depto_id = departamentos.id;
```

### 3.2 **Subconsultas (Subqueries)**
```sql
-- Subconsulta en la cláusula WHERE
SELECT nombre FROM empleados WHERE salario > (SELECT AVG(salario) FROM empleados);
```

### 3.3 **Agrupar Resultados (GROUP BY)**
```sql
-- Agrupar por una columna
SELECT departamento, AVG(salario) FROM empleados GROUP BY departamento;
```

### 3.4 **Filtrar Después de Agrupar (HAVING)**
```sql
-- Filtrar después de agrupar
SELECT departamento, AVG(salario) FROM empleados GROUP BY departamento HAVING AVG(salario) > 3500;
```

---

## 4. **Operaciones de Modificación de Datos**

### 4.1 **INSERTAR Datos**
```sql
-- Insertar un nuevo registro
INSERT INTO empleados (nombre, salario, depto_id) VALUES ('Carlos', 4500, 3);
```

### 4.2 **ACTUALIZAR Datos**
```sql
-- Actualizar un registro existente
UPDATE empleados SET salario = 5000 WHERE nombre = 'Carlos';
```

### 4.3 **BORRAR Datos**
```sql
-- Eliminar un registro
DELETE FROM empleados WHERE nombre = 'Carlos';
```

---

## 5. **Índices y Optimización**

### 5.1 **Índices**
- **Índice**: Estructura que mejora la velocidad de las consultas.
```sql
-- Crear un índice en una columna
CREATE INDEX idx_salario ON empleados(salario);
```

### 5.2 **Optimización de Consultas**
- Evitar usar `SELECT *` en producción.
- Utilizar índices para mejorar el rendimiento de las consultas más frecuentes.
- Asegurarse de utilizar `WHERE` para filtrar resultados y no cargar toda la tabla.

---

## 6. **Transacciones**

### 6.1 **Control de Transacciones**
```sql
-- Iniciar una transacción
BEGIN TRANSACTION;

-- Realizar varias operaciones
UPDATE empleados SET salario = 5500 WHERE nombre = 'Carlos';

-- Confirmar los cambios
COMMIT;

-- Si ocurre un error, revertir los cambios
ROLLBACK;
```

---

## 7. **Funciones y Procedimientos Almacenados**

### 7.1 **Crear Función**
```sql
CREATE FUNCTION calcular_bonus(salario DECIMAL) RETURNS DECIMAL AS $$
BEGIN
  RETURN salario * 0.1;
END;
$$ LANGUAGE plpgsql;
```

### 7.2 **Crear Procedimiento Almacenado**
```sql
CREATE PROCEDURE actualizar_salario()
AS $$
BEGIN
  UPDATE empleados SET salario = salario * 1.05;
END;
$$ LANGUAGE plpgsql;
```

---

## 8. **Consideraciones de Seguridad**

### 8.1 **Acceso a Datos**
- Utilizar roles para controlar el acceso a la base de datos.
- **GRANT**: Otorgar permisos a un usuario.
```sql
GRANT SELECT, INSERT ON empleados TO usuario_trainee;
```

### 8.2 **Auditoría de Consultas**
- Monitorear consultas y accesos a datos sensibles.

---

## 9. **Consideraciones para Big Data**

- Si trabajas con **bases de datos distribuidas** (como Hadoop o Spark SQL), algunas operaciones en SQL pueden tener diferencias importantes, como el uso de **particiones** y **optimizadores de consultas**.
- Trabajar con **SQL en la nube** (AWS RDS, Google Cloud SQL, Azure SQL Database) puede requerir configuraciones específicas.
