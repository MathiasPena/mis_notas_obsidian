## 1. **MapReduce**

**MapReduce** es un modelo de programación distribuido que permite procesar grandes volúmenes de datos de manera paralela en un clúster de computadoras. Originalmente diseñado por Google, es ampliamente utilizado en plataformas como **Hadoop** para el procesamiento de datos a gran escala.

### **Funcionamiento básico de MapReduce:**

El modelo de programación MapReduce se divide en dos fases principales:

1. **Fase de Map (Map):**
   - Los datos se dividen en fragmentos, y cada fragmento se procesa de manera independiente por el mapeador.
   - Cada mapeador toma un conjunto de datos (generalmente en formato de pares clave-valor) y genera nuevos pares clave-valor como resultado de la operación.
   - Los mapeadores son responsables de filtrar y transformar los datos.

2. **Fase de Reduce (Reduce):**
   - Los pares clave-valor generados en la fase de Map son agrupados por claves.
   - Los reductores toman todos los valores asociados con una clave específica y los combinan (por ejemplo, sumando, promediando, etc.) para obtener el resultado final.

### **Ejemplo de MapReduce:**
Supongamos que tenemos un archivo de texto con varias palabras y queremos contar cuántas veces aparece cada palabra en el archivo.

**Entrada (Archivo de texto):**
```
apple banana apple grape banana apple
```

#### **Fase Map:**
En la fase Map, el archivo se divide en fragmentos y se procesan de manera independiente. El mapeador toma las palabras y las convierte en pares clave-valor.

```plaintext
("apple", 1)
("banana", 1)
("apple", 1)
("grape", 1)
("banana", 1)
("apple", 1)
```

#### **Fase Reduce:**
En la fase Reduce, los pares clave-valor generados en la fase Map se agrupan por clave, y el reductor suma los valores asociados a cada clave.

```plaintext
("apple", 3)
("banana", 2)
("grape", 1)
```

#### **Código básico de MapReduce en Hadoop (en Java):**

```java
// Mapper
public class WordCountMapper extends Mapper<LongWritable, Text, Text, IntWritable> {
    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();
    
    public void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
        String[] words = value.toString().split("\\s+");
        for (String w : words) {
            word.set(w);
            context.write(word, one);
        }
    }
}

// Reducer
public class WordCountReducer extends Reducer<Text, IntWritable, Text, IntWritable> {
    private IntWritable result = new IntWritable();
    
    public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
            sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
}
```

#### **Ventajas de MapReduce:**
1. **Escalabilidad:** Puede procesar grandes volúmenes de datos en paralelo, aprovechando un clúster de máquinas.
2. **Simplicidad:** Es fácil de entender y usar para tareas de procesamiento en lotes.
3. **Tolerancia a fallos:** Si un nodo falla, MapReduce puede reintentar las tareas fallidas en otros nodos del clúster.

#### **Desventajas de MapReduce:**
1. **Lento:** El procesamiento por lotes y las múltiples fases (Map y Reduce) pueden hacerlo más lento en comparación con otros enfoques de procesamiento en tiempo real, como Spark.
2. **Limitado para tareas interactivas:** No es adecuado para análisis interactivos o procesamiento en tiempo real debido a su naturaleza por lotes.
3. **Complejidad en tareas complejas:** Para trabajos complejos o que requieren varias etapas de procesamiento, MapReduce puede ser más difícil de implementar y mantener.

---

### **Alternativa a MapReduce:**
En plataformas más modernas, como **Apache Spark**, MapReduce ha sido reemplazado por **RDDs** (Resilient Distributed Datasets), que permiten un procesamiento más eficiente, especialmente cuando se trata de tareas complejas y en memoria.
