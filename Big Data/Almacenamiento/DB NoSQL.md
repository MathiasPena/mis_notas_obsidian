## 3. **Bases de datos NoSQL (MongoDB, Cassandra, HBase)**

Las bases de datos **NoSQL** son sistemas de gestión de bases de datos diseñados para almacenar, procesar y gestionar grandes volúmenes de datos no estructurados o semi-estructurados. A diferencia de las bases de datos relacionales, las bases de datos NoSQL no utilizan tablas y relaciones de manera estricta. Son escalables y pueden manejar diferentes tipos de datos, lo que las hace ideales para Big Data.

### **Principales Tipos de Bases de Datos NoSQL**
Existen varios tipos de bases de datos NoSQL, pero los más comunes son:

1. **Bases de datos de documentos:** Almacenan datos en formato de documentos (por ejemplo, JSON o BSON), en lugar de filas y columnas. Cada documento es autónomo y puede tener una estructura diferente. Ejemplo: **MongoDB**.
2. **Bases de datos de clave-valor:** Almacenan pares clave-valor, donde cada clave única está asociada a un valor. Este tipo es muy eficiente para búsquedas rápidas y datos simples. Ejemplo: **Redis**.
3. **Bases de datos de columnas:** Organizan los datos en columnas en lugar de filas, lo que es útil para consultas en grandes volúmenes de datos. Ejemplo: **Cassandra**.
4. **Bases de datos de grafos:** Están optimizadas para almacenar relaciones entre los datos y se utilizan principalmente en aplicaciones que requieren modelar relaciones complejas entre datos. Ejemplo: **Neo4j**.

### **Bases de datos NoSQL más comunes:**

#### **MongoDB**
MongoDB es una base de datos orientada a documentos que almacena los datos en formato JSON o BSON. Está diseñada para aplicaciones web y móviles que requieren flexibilidad, escalabilidad y velocidad. 

**Características clave de MongoDB:**
- **Modelo flexible:** Al ser orientada a documentos, no es necesario definir un esquema rígido antes de almacenar los datos. Puedes almacenar documentos con diferentes estructuras en la misma colección.
- **Escalabilidad horizontal:** MongoDB puede escalar de manera horizontal, lo que significa que puede distribuir los datos en varios servidores para aumentar la capacidad de almacenamiento y procesamiento.
- **Alta disponibilidad:** MongoDB permite la replicación de datos en múltiples servidores, lo que asegura que los datos estén disponibles incluso si un servidor falla.

**Ejemplo de documento en MongoDB (en formato JSON):**
```json
{
  "_id": "12345",
  "nombre": "Juan Perez",
  "edad": 30,
  "direccion": {
    "calle": "Av. Libertador",
    "ciudad": "Montevideo"
  }
}
```

**Operaciones comunes en MongoDB:**
- **Insertar documento:** `db.coleccion.insert({ campo1: valor1, campo2: valor2 })`
- **Encontrar documento:** `db.coleccion.find({ campo: valor })`
- **Actualizar documento:** `db.coleccion.update({ campo: valor }, { $set: { campo2: valor2 }})`
- **Eliminar documento:** `db.coleccion.remove({ campo: valor })`

#### **Cassandra**
Apache Cassandra es una base de datos distribuida diseñada para manejar grandes cantidades de datos en entornos de Big Data. Está diseñada para ser escalable, tolerante a fallos y para ofrecer una alta disponibilidad.

**Características clave de Cassandra:**
- **Escalabilidad masiva:** Cassandra puede escalar horizontalmente sin perder rendimiento, lo que la hace ideal para aplicaciones que requieren almacenar grandes volúmenes de datos.
- **Tolerancia a fallos:** Cassandra replica datos en múltiples nodos para garantizar que los datos no se pierdan si un nodo falla.
- **Modelo basado en columnas:** En lugar de filas, Cassandra organiza los datos en columnas, lo que mejora el rendimiento en consultas que involucran grandes volúmenes de datos.

**Ejemplo de esquema en Cassandra:**
```sql
CREATE TABLE usuarios (
  id UUID PRIMARY KEY,
  nombre TEXT,
  edad INT,
  direccion TEXT
);
```

**Operaciones comunes en Cassandra:**
- **Insertar datos:** `INSERT INTO usuarios (id, nombre, edad, direccion) VALUES (uuid(), 'Juan Perez', 30, 'Av. Libertador')`
- **Consultar datos:** `SELECT * FROM usuarios WHERE id = ?`
- **Actualizar datos:** `UPDATE usuarios SET edad = 31 WHERE id = ?`
- **Eliminar datos:** `DELETE FROM usuarios WHERE id = ?`

#### **HBase**
HBase es una base de datos de columnas que está diseñada para manejar grandes volúmenes de datos distribuidos en entornos de Big Data, y está inspirada en Google Bigtable. HBase se integra de forma nativa con el ecosistema Hadoop.

**Características clave de HBase:**
- **Modelo basado en columnas:** Los datos se almacenan en tablas con filas y columnas, pero se accede a ellos por columnas.
- **Escalabilidad:** HBase puede almacenar petabytes de datos y puede escalar de manera horizontal al agregar más nodos.
- **Integración con Hadoop:** HBase es ideal para almacenar grandes volúmenes de datos no estructurados y se puede integrar fácilmente con Hadoop para el procesamiento distribuido.

**Ejemplo de creación de tabla en HBase:**
```bash
create 'usuarios', 'informacion_personal', 'direccion'
```

**Operaciones comunes en HBase:**
- **Insertar datos:** `put 'usuarios', 'row1', 'informacion_personal:nombre', 'Juan Perez'`
- **Consultar datos:** `get 'usuarios', 'row1'`
- **Actualizar datos:** `put 'usuarios', 'row1', 'informacion_personal:edad', '31'`
- **Eliminar datos:** `delete 'usuarios', 'row1'`

---

### **Relación con Apache Spark**
Las bases de datos NoSQL, como MongoDB, Cassandra y HBase, se integran de forma efectiva con Apache Spark para realizar análisis de Big Data. Spark puede acceder a estos sistemas de almacenamiento distribuido para realizar procesamiento en memoria y de alto rendimiento. 

- **MongoDB y Spark:** Puedes usar el conector MongoDB para Spark, que permite que Spark lea y escriba datos directamente en MongoDB.
- **Cassandra y Spark:** Cassandra tiene un conector nativo para Spark, que permite leer y escribir datos en Cassandra utilizando el poder de procesamiento distribuido de Spark.
- **HBase y Spark:** Apache Spark puede integrarse con HBase para procesar grandes volúmenes de datos almacenados en HBase, usando el conector de HBase para Spark.
