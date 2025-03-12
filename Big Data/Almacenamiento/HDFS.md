## 2. **HDFS (Hadoop Distributed File System)**

### **¿Qué es HDFS?**
**HDFS (Hadoop Distributed File System)** es un sistema de almacenamiento distribuido diseñado para almacenar grandes volúmenes de datos en una red de máquinas. Forma parte del ecosistema de Hadoop y está optimizado para almacenar datos de forma confiable en un entorno distribuido, a la vez que proporciona acceso rápido a esos datos para su procesamiento. HDFS permite que los datos se dividan en bloques grandes, los cuales son replicados y distribuidos por varias máquinas en un clúster, garantizando la disponibilidad y la tolerancia a fallos.

### **Arquitectura de HDFS**
La arquitectura de HDFS está basada en una arquitectura maestro-esclavo, con dos componentes principales:

1. **NameNode (Maestro):** Es el nodo principal que administra el sistema de archivos. Mantiene el **metadato** de los archivos, como las ubicaciones de los bloques, permisos de acceso, y estructura del directorio. El NameNode no almacena los datos en sí, sino solo los metadatos que indican dónde se encuentran los bloques de datos.
   
2. **DataNode (Esclavos):** Son los nodos que almacenan los bloques de datos reales. Cada DataNode es responsable de almacenar y gestionar los bloques de datos en su máquina local. Además, también realiza tareas como la replicación de bloques de datos para asegurar la tolerancia a fallos.

**Estructura de almacenamiento en HDFS:**
- Los datos son **divididos** en bloques de un tamaño grande (normalmente 128 MB o 256 MB).
- Estos bloques son replicados (por defecto, 3 copias) y distribuidos a través de los DataNodes del clúster, lo que garantiza la **alta disponibilidad** y la **tolerancia a fallos**.

### **Características de HDFS**
- **Escalabilidad:** HDFS puede escalar fácilmente agregando más nodos al clúster.
- **Tolerancia a fallos:** Los bloques de datos se replican en diferentes nodos, lo que asegura que si un nodo falla, los datos aún estarán disponibles en otros nodos.
- **Rendimiento:** HDFS está optimizado para leer y escribir grandes volúmenes de datos, lo que lo hace ideal para almacenar y procesar Big Data.
- **Costo bajo:** Debido a su arquitectura distribuida y uso de hardware de bajo costo, HDFS es más económico en comparación con otros sistemas de almacenamiento centralizados.

### **Operaciones comunes en HDFS**
- **Lectura de datos:** Los clientes leen bloques de datos de los DataNodes a través del NameNode.
- **Escritura de datos:** Los datos se dividen en bloques y se distribuyen entre los DataNodes, asegurando que cada bloque se replique.
- **Replicación de bloques:** El sistema asegura que los bloques de datos estén replicados en múltiples DataNodes para evitar pérdidas en caso de fallos.

### **Ventajas de HDFS**
1. **Alta disponibilidad:** Gracias a la replicación de bloques, HDFS garantiza que los datos estén disponibles incluso si un nodo falla.
2. **Alta escalabilidad:** Al ser un sistema distribuido, HDFS puede escalar para manejar grandes volúmenes de datos agregando más nodos al clúster.
3. **Eficiencia en grandes volúmenes de datos:** Está optimizado para almacenar y procesar grandes cantidades de datos, lo que lo hace ideal para Big Data.

### **Desventajas de HDFS**
1. **Latencia:** HDFS no está optimizado para operaciones de baja latencia, como las transacciones rápidas de bases de datos.
2. **Tamaño de archivo:** HDFS está diseñado para manejar grandes archivos de datos, por lo que no es ideal para archivos pequeños o operaciones frecuentes de lectura/escritura de pequeños archivos.

### **Relación con Apache Spark**
HDFS y Apache Spark suelen trabajar juntos en el ecosistema de Big Data. HDFS proporciona el almacenamiento distribuido para los grandes volúmenes de datos que Spark procesa. Spark puede acceder directamente a los datos almacenados en HDFS para realizar operaciones de procesamiento de datos en paralelo y a gran escala. 

Cuando Spark procesa datos, divide las tareas de procesamiento entre múltiples nodos en un clúster, aprovechando tanto el almacenamiento distribuido de HDFS como la capacidad de procesamiento distribuido de Spark. Spark puede usar HDFS como su sistema de almacenamiento de datos en conjunto con su capacidad de procesamiento en memoria, lo que lo convierte en una opción poderosa para análisis de Big Data.
