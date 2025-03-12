## 3. **DataFrames y Datasets en Spark**

Los **DataFrames** y **Datasets** son abstracciones más avanzadas que los **RDDs** en Apache Spark. Están diseñados para ser más fáciles de usar, más eficientes y con una mejor integración con las optimizaciones de Spark. A diferencia de los **RDDs**, estos permiten un procesamiento estructurado, lo que facilita la manipulación y consulta de grandes volúmenes de datos de manera distribuida.

### **DataFrames:**

Un **DataFrame** es una estructura de datos distribuida que se asemeja a una tabla en una base de datos relacional o a un dataframe en Pandas. Los DataFrames en Spark están diseñados para trabajar con datos estructurados y proporcionan una API de alto nivel para realizar operaciones de transformación y agregación.

#### **Características de los DataFrames:**
1. **Estructurados:**
   - Los DataFrames están formados por columnas con nombres y tipos de datos definidos.
2. **Optimización:**
   - Spark optimiza las operaciones sobre DataFrames usando su motor de ejecución Catalyst, lo que permite mejoras automáticas en el rendimiento.
3. **Interoperabilidad:**
   - Los DataFrames en Spark pueden ser creados a partir de RDDs, bases de datos, archivos CSV, JSON, Parquet, etc.
4. **Lenguaje de consulta similar a SQL:**
   - Puedes usar **Spark SQL** para realizar consultas sobre DataFrames de manera similar a SQL.

#### **Operaciones comunes en DataFrames:**

- **Creación de DataFrame:**
  Puedes crear un DataFrame a partir de un RDD, un archivo CSV, Parquet, JSON, entre otros.

  **Ejemplo:**
  ```python
  # Crear DataFrame desde una lista
  from pyspark.sql import SparkSession
  spark = SparkSession.builder.appName("DataFrameExample").getOrCreate()
  data = [("Alice", 25), ("Bob", 30), ("Cathy", 29)]
  df = spark.createDataFrame(data, ["Name", "Age"])
  df.show()
  ```

- **Selección de columnas:**
  Puedes seleccionar columnas de un DataFrame utilizando el nombre de las columnas o usando expresiones.

  **Ejemplo:**
  ```python
  df.select("Name").show()  # Seleccionar solo la columna 'Name'
  ```

- **Filtrar datos:**
  Puedes aplicar filtros a un DataFrame usando `filter` o `where`.

  **Ejemplo:**
  ```python
  df.filter(df.Age > 25).show()  # Filtrar por edad mayor a 25
  ```

- **Agregar nuevas columnas:**
  Puedes agregar columnas calculadas a un DataFrame.

  **Ejemplo:**
  ```python
  df.withColumn("AgeIn5Years", df.Age + 5).show()
  ```

- **Agrupar y contar:**
  Puedes realizar operaciones de agregación como `count`, `sum`, `avg`, etc.

  **Ejemplo:**
  ```python
  df.groupBy("Age").count().show()  # Agrupar por 'Age' y contar
  ```

#### **Ventajas de usar DataFrames:**
- **Optimización interna:**
  Spark puede optimizar consultas sobre DataFrames usando su optimizador **Catalyst**.
- **API fácil de usar:**
  La API de DataFrames proporciona métodos fáciles de leer y usar, como `.show()`, `.select()`, y `.filter()`.
- **Compatibilidad con SQL:**
  Puedes ejecutar consultas SQL directamente sobre un DataFrame usando la función `spark.sql()`.

---

### **Datasets:**

El **Dataset** es una abstracción similar al **DataFrame** pero con la diferencia de que está fuertemente tipado. Es una API que combina las ventajas de RDDs (tipado estático) con las optimizaciones de los DataFrames (consultas estructuradas).

#### **Características de los Datasets:**
1. **Tipado Estático:**
   - Los **Datasets** en Spark tienen un tipo de datos definido, lo que permite trabajar con datos de una manera más estructurada y segura en comparación con los DataFrames.
   
2. **Transformaciones de tipo RDD y DataFrame:**
   - Puedes aplicar operaciones tanto de **RDDs** como de **DataFrames** a un **Dataset**.

3. **Interoperabilidad con DataFrames:**
   - Un **Dataset** es básicamente un **DataFrame** con un tipo de datos adicional. Puedes convertir entre ambos fácilmente.

#### **Operaciones comunes en Datasets:**

- **Creación de un Dataset:**
  Los **Datasets** son creados a partir de objetos Java o Scala, pero en PySpark solo tenemos soporte para **DataFrames**. Sin embargo, los DataFrames en PySpark se pueden ver como una representación de los **Datasets** en Java/Scala.

  **Ejemplo en Scala:**
  ```scala
  case class Person(name: String, age: Int)
  val people = Seq(Person("Alice", 25), Person("Bob", 30))
  val ds = spark.createDataset(people)
  ds.show()
  ```

- **Operaciones de transformación:**
  Las operaciones sobre **Datasets** son similares a las de los **DataFrames**. Puedes aplicar transformaciones como `map`, `filter`, `select`, etc.

  **Ejemplo:**
  ```scala
  ds.filter(_.age > 25).show()
  ```

#### **Ventajas de los Datasets:**
- **Seguridad de tipo:**
  Los **Datasets** proporcionan un tipo de datos seguro, lo que significa que el compilador puede detectar errores de tipo en tiempo de compilación (en Scala o Java).
- **Mejor integración con el sistema de tipos:**
  Como los **Datasets** son más estructurados, permiten una mejor integración con las funciones específicas del lenguaje de programación, como el uso de objetos y clases.
- **Optimización:**
  Al igual que los **DataFrames**, los **Datasets** también se benefician del optimizador Catalyst para consultas SQL.

---

### **Diferencias clave entre RDD, DataFrame y Dataset:**

| Característica                  | **RDD**                    | **DataFrame**                | **Dataset**               |
|----------------------------------|----------------------------|------------------------------|---------------------------|
| **Tipado**                       | No tipado (diferente en cada operación) | No tipado (pero optimizado para operaciones SQL) | Tipado estático (Java/Scala) |
| **API**                          | Bajo nivel, flexible, pero más compleja | Alto nivel, fácil de usar, optimizado | Alto nivel, pero con más seguridad de tipo |
| **Optimización**                 | No optimizado              | Optimizado mediante Catalyst  | Optimizado mediante Catalyst |
| **Facilidad de uso**             | Más complejo               | Fácil de usar, SQL-like       | Fácil de usar, pero con seguridad de tipo |
| **Tolerancia a fallos**          | Alta                       | Alta                         | Alta                      |

---

**Los DataFrames** y **Datasets** ofrecen un enfoque más eficiente y fácil de usar para el procesamiento de datos en Apache Spark en comparación con los **RDDs**. Aunque los RDDs proporcionan un control más detallado, los DataFrames y Datasets son generalmente preferidos para trabajar con grandes volúmenes de datos estructurados y permiten un procesamiento más optimizado y manejable.
