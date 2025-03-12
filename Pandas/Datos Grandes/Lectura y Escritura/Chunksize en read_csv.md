
Cuando trabajas con **grandes volúmenes de datos** en **Pandas**, es importante usar métodos que te ayuden a gestionar la memoria y a optimizar el rendimiento. Una de las técnicas más útiles para leer archivos grandes es el uso de **`chunksize`** en la función **`read_csv()`**.

### **chunksize en read_csv()**

La opción **`chunksize`** en **`read_csv()`** permite leer un archivo grande en **fragmentos (chunks)** más pequeños en lugar de cargar todo el archivo de una vez en memoria. Esta técnica es útil cuando los archivos no caben completamente en la memoria o cuando quieres procesar datos en bloques más pequeños.

#### Sintaxis:
```python
pd.read_csv('archivo.csv', chunksize=10000)
```

- **`chunksize`**: Especifica el tamaño del fragmento en número de filas. En este caso, Pandas leerá el archivo en bloques de 10,000 filas a la vez.

#### Ejemplo:
```python
import pandas as pd

# Leer archivo CSV en fragmentos de 10000 filas
chunk_iter = pd.read_csv('gran_archivo.csv', chunksize=10000)

# Iterar sobre cada fragmento
for chunk in chunk_iter:
    # Realiza operaciones sobre cada fragmento de datos
    print(chunk.head())  # Imprime las primeras 5 filas de cada fragmento
```

En este ejemplo, **`read_csv()`** se usa con **`chunksize`** para leer el archivo en bloques de 10,000 filas. Luego, puedes iterar sobre cada **chunk** y realizar las operaciones necesarias en cada uno, sin cargar todo el archivo en memoria al mismo tiempo.

### **Ventajas del uso de chunksize**

1. **Reducción del uso de memoria**: Al leer solo un fragmento de los datos a la vez, puedes trabajar con archivos más grandes que no caben completamente en memoria.
2. **Procesamiento en paralelo o por lotes**: Si necesitas realizar una operación costosa sobre un archivo grande, puedes dividirla en bloques más pequeños para procesarlas de manera más eficiente.
3. **Optimización de rendimiento**: Al trabajar con **fragmentos** de datos, puedes realizar las operaciones sobre cada uno y liberar la memoria de forma más eficiente.

### **Consideraciones**

- El **`chunksize`** debe ser ajustado según la memoria disponible en tu sistema. Si el tamaño de cada fragmento es demasiado grande, puedes terminar agotando la memoria, aunque el archivo no se lea completamente a la vez.
- Después de procesar cada **chunk**, puedes realizar operaciones como concatenar, agrupar, o escribir los resultados en otro archivo.

#### Ejemplo con procesamiento y escritura:
```python
import pandas as pd

# Iterar sobre el archivo CSV en fragmentos de 10000 filas
chunk_iter = pd.read_csv('gran_archivo.csv', chunksize=10000)

# Crear un archivo de salida vacío
with open('resultado.csv', 'w') as outfile:
    for chunk in chunk_iter:
        # Realizar operaciones en el fragmento
        processed_chunk = chunk[chunk['columna'] > 10]  # Filtrar datos
        # Escribir los fragmentos procesados en un archivo de salida
        processed_chunk.to_csv(outfile, header=outfile.tell() == 0, index=False)
```

En este ejemplo, los datos se filtran y luego se escriben en un archivo **`resultado.csv`** en fragmentos, evitando cargar todo el archivo en memoria.

### **Conclusión**

El uso de **`chunksize`** en **`read_csv()`** es una herramienta poderosa cuando trabajas con archivos grandes en **Pandas**. Permite gestionar mejor el uso de memoria y optimiza el procesamiento de datos dividiéndolos en bloques más pequeños. Este enfoque es ideal para tareas como análisis de grandes volúmenes de datos, procesamiento por lotes y escritura eficiente en nuevos archivos.
