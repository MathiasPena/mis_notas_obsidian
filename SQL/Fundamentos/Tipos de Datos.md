
En SQL, los tipos de datos definen el tipo de valor que una columna puede almacenar. Elegir el tipo de dato adecuado es crucial para garantizar un buen rendimiento y la integridad de los datos.

## **1. INT (Enteros)**

El tipo **`INT`** se usa para almacenar números enteros. Existen variantes como **`TINYINT`**, **`SMALLINT`**, **`MEDIUMINT`**, **`BIGINT`** que permiten almacenar números enteros en diferentes rangos de tamaño.

- **Tamaño**: 4 bytes.
- **Rango (por defecto)**: De -2,147,483,648 a 2,147,483,647.
  
### Ejemplo:
```sql
CREATE TABLE ejemplo (
    id INT
);
```

## **2. VARCHAR (Cadenas de texto)**

**`VARCHAR`** se utiliza para almacenar cadenas de texto de longitud variable. El número máximo de caracteres debe ser especificado al momento de la creación de la columna.

- **Tamaño**: Variable, según el número de caracteres especificado.
- **Rango**: Puede almacenar hasta 65,535 caracteres, dependiendo del tipo de base de datos.

### Ejemplo:
```sql
CREATE TABLE ejemplo (
    nombre VARCHAR(100)
);
```

## **3. TEXT (Texto largo)**

El tipo **`TEXT`** se utiliza para almacenar cadenas de texto de longitud variable, pero a diferencia de **`VARCHAR`**, **`TEXT`** está destinado a almacenar textos muy largos.

- **Tamaño**: 4 GB de almacenamiento.
- **Rango**: Ideal para textos largos como descripciones, comentarios, artículos, etc.

### Ejemplo:
```sql
CREATE TABLE ejemplo (
    descripcion TEXT
);
```

## **4. DATE (Fechas)**

El tipo **`DATE`** se utiliza para almacenar fechas en formato **`YYYY-MM-DD`**.

- **Tamaño**: 3 bytes.
- **Rango**: De '1000-01-01' a '9999-12-31'.

### Ejemplo:
```sql
CREATE TABLE ejemplo (
    fecha_nacimiento DATE
);
```

## **5. DECIMAL (Números decimales)**

**`DECIMAL`** se utiliza para almacenar números con precisión exacta. Es especialmente útil cuando se necesitan manejar valores financieros o de medición exactos.

- **Tamaño**: Define la precisión y escala como **`DECIMAL(p, s)`**, donde **`p`** es la precisión (número total de dígitos) y **`s`** es la escala (número de dígitos a la derecha del punto decimal).
- **Ejemplo de precisión**: **`DECIMAL(10, 2)`** puede almacenar números de hasta 10 dígitos, con 2 dígitos después del punto decimal.

### Ejemplo:
```sql
CREATE TABLE ejemplo (
    salario DECIMAL(10, 2)
);
```

## **6. BOOLEAN (Booleano)**

El tipo **`BOOLEAN`** almacena valores **`TRUE`** o **`FALSE`**. Dependiendo del sistema de base de datos, se puede almacenar como **`TINYINT(1)`** (donde 0 es **`FALSE`** y 1 es **`TRUE`**).

- **Tamaño**: 1 byte.
- **Rango**: **`TRUE`** o **`FALSE`** (internamente puede ser representado como 1 o 0).

### Ejemplo:
```sql
CREATE TABLE ejemplo (
    es_activo BOOLEAN
);
```

## **Conclusión**

Elegir el tipo de dato adecuado para cada columna de una base de datos es fundamental para la optimización de la memoria, el rendimiento y la integridad de los datos. Cada tipo de dato tiene sus ventajas y debe ser usado según las necesidades del negocio y el tipo de dato que se desea almacenar.
