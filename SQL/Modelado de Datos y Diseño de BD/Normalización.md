# Modelado de Datos y Diseño de Bases de Datos

## Normalización (1FN, 2FN, 3FN, BCNF)

La **normalización** es el proceso de estructurar una base de datos para reducir la redundancia de datos y mejorar la integridad de los mismos. Se divide en diferentes **formas normales (FN)**, que son reglas que ayudan a organizar las tablas de manera eficiente. El objetivo es dividir la base de datos en varias tablas pequeñas y eliminar las dependencias no deseadas.

### **1. Primera Forma Normal (1FN)**

Una tabla está en **1FN** si cumple con las siguientes condiciones:
- Cada columna contiene valores atómicos (es decir, no puede haber listas, arreglos o conjuntos de datos en una sola celda).
- Todos los valores en una columna son del mismo tipo.
- Cada fila tiene una clave primaria única.

#### Ejemplo:
| ID  | Nombre     | Teléfonos           |
|-----|------------|---------------------|
| 1   | Juan       | 555-1234, 555-5678  |
| 2   | Ana        | 555-8765            |

Para que la tabla esté en **1FN**, eliminamos los valores repetidos en la columna **Teléfonos**:

| ID  | Nombre     | Teléfono  |
|-----|------------|-----------|
| 1   | Juan       | 555-1234  |
| 1   | Juan       | 555-5678  |
| 2   | Ana        | 555-8765  |

Ahora, cada celda contiene un solo valor y cada fila es única.

### **2. Segunda Forma Normal (2FN)**

Una tabla está en **2FN** si está en **1FN** y todos los atributos no clave dependen completamente de la clave primaria (es decir, no hay dependencias parciales).

#### Ejemplo:
Supongamos que tenemos la siguiente tabla de ventas:

| ID_venta | Producto  | Precio | Cantidad | Total  |
|----------|-----------|--------|----------|--------|
| 1        | Manzana   | 1.5    | 3        | 4.5    |
| 2        | Plátano   | 1.0    | 5        | 5.0    |

La columna **Total** depende de **Precio** y **Cantidad**, pero no de **ID_venta**. Para cumplir con **2FN**, descomponemos la tabla en dos:

**Ventas**:

| ID_venta | Producto  | Cantidad |
|----------|-----------|----------|
| 1        | Manzana   | 3        |
| 2        | Plátano   | 5        |

**Precios**:

| Producto  | Precio |
|-----------|--------|
| Manzana   | 1.5    |
| Plátano   | 1.0    |

Ahora, **Total** puede calcularse usando una consulta que relacione ambas tablas. Cada tabla tiene una clave primaria única y todas las columnas dependen completamente de esa clave.

### **3. Tercera Forma Normal (3FN)**

Una tabla está en **3FN** si está en **2FN** y no tiene dependencias transitivas, es decir, no hay dependencias entre atributos no clave.

#### Ejemplo:
Supongamos que tenemos la siguiente tabla de empleados:

| ID_empleado | Nombre  | Departamento | Jefe       | Jefe_Departamento |
|-------------|---------|--------------|------------|-------------------|
| 1           | Juan    | IT           | Pedro      | IT                |
| 2           | Ana     | HR           | Maria      | HR                |

La columna **Jefe_Departamento** depende de **Jefe**, que a su vez depende de **Departamento**, lo que crea una dependencia transitoria. Para cumplir con **3FN**, dividimos la tabla en dos:

**Empleados**:

| ID_empleado | Nombre  | Departamento | Jefe       |
|-------------|---------|--------------|------------|
| 1           | Juan    | IT           | Pedro      |
| 2           | Ana     | HR           | Maria      |

**Departamentos**:

| Departamento | Jefe       |
|--------------|------------|
| IT           | Pedro      |
| HR           | Maria      |

Ahora, eliminamos la dependencia transitiva, y cada columna depende solo de la clave primaria.

### **4. Forma Normal de Boyce-Codd (BCNF)**

Una tabla está en **BCNF** si está en **3FN** y para cada una de sus dependencias funcionales, la determinante (el atributo que determina el valor de otro atributo) es una clave candidata. Es una versión más estricta de **3FN**.

#### Ejemplo:
Supongamos que tenemos una tabla de cursos y estudiantes:

| ID_estudiante | ID_curso | Profesor   |
|---------------|----------|------------|
| 1             | 101      | Dr. Pérez  |
| 2             | 102      | Dra. Gómez |

Si **ID_curso** determina **Profesor**, pero **ID_estudiante** no determina **ID_curso**, la tabla no está en **BCNF**. Para llevarla a **BCNF**, se tendría que dividir en dos tablas:

**Estudiantes_Cursos**:

| ID_estudiante | ID_curso |
|---------------|----------|
| 1             | 101      |
| 2             | 102      |

**Cursos_Profesores**:

| ID_curso | Profesor   |
|----------|------------|
| 101      | Dr. Pérez  |
| 102      | Dra. Gómez |

Ahora, tanto **ID_curso** como **ID_estudiante** determinan únicamente sus respectivas columnas y la tabla está en **BCNF**.

## Resumen de las Formas Normales:
- **1FN**: Cada columna tiene valores atómicos.
- **2FN**: Está en **1FN** y no hay dependencias parciales.
- **3FN**: Está en **2FN** y no tiene dependencias transitivas.
- **BCNF**: Está en **3FN** y todas las dependencias son de claves candidatas.

## Beneficios de la Normalización:
- **Reducción de redundancia**: Menos duplicación de datos.
- **Mejora de integridad**: Más control sobre la consistencia de los datos.
- **Facilita el mantenimiento**: Las actualizaciones, eliminaciones e inserciones son más fáciles y consistentes.

## Desventajas:
- **Complejidad en las consultas**: Se pueden requerir múltiples uniones (**JOIN**) entre tablas.
- **Rendimiento**: Las bases de datos muy normalizadas pueden ser menos eficientes en términos de rendimiento debido a la necesidad de realizar múltiples uniones.

La normalización es esencial para garantizar una estructura de base de datos eficiente y evitar problemas de consistencia, pero siempre debe equilibrarse con las necesidades específicas de rendimiento de la aplicación.
