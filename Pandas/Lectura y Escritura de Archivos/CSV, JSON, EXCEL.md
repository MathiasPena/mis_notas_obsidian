
Pandas ofrece funciones muy eficientes para leer y escribir archivos CSV. Es uno de los formatos más comunes para almacenar datos tabulares.

### **Leer un archivo CSV**

La función **`pd.read_csv()`** se usa para leer archivos CSV. Pandas convierte automáticamente las filas y columnas del CSV en un `DataFrame`.

```python
import pandas as pd

# Leer archivo CSV
df = pd.read_csv('archivo.csv')

# Mostrar las primeras filas
print(df.head())
```

### **Escribir un DataFrame a un archivo CSV**

Para guardar un `DataFrame` en un archivo CSV, se usa el método **`.to_csv()`**. Puedes elegir si quieres incluir el índice en el archivo.

```python
# Escribir DataFrame a CSV
df.to_csv('archivo_guardado.csv', index=False)
```

#### **Parámetros útiles de `read_csv()` y `to_csv()`**
- **`index_col`**: Especifica qué columna usar como índice.
- **`header`**: Define qué fila usar como cabecera (por defecto es la primera).
- **`sep`**: Define el delimitador (por defecto es `,`, pero puede ser cualquier delimitador como tabuladores `\t`).
  
Ejemplo con parámetros:

```python
# Leer CSV con delimitador de tabulador
df = pd.read_csv('archivo.tsv', sep='\t')

# Guardar DataFrame sin índice
df.to_csv('archivo_sin_indice.csv', index=False)
```

---

## 🔹 **Excel (`pd.read_excel()`, `.to_excel()`)**

Pandas permite trabajar con archivos Excel a través de **`read_excel()`** y **`to_excel()`**.

### **Leer un archivo Excel**

Usando **`pd.read_excel()`** podemos leer hojas de cálculo Excel. Se puede especificar el nombre de la hoja con el parámetro `sheet_name`.

```python
# Leer archivo Excel
df = pd.read_excel('archivo.xlsx', sheet_name='Hoja1')

# Mostrar las primeras filas
print(df.head())
```

### **Escribir un DataFrame a un archivo Excel**

La función **`.to_excel()`** guarda un `DataFrame` en un archivo Excel. Puedes elegir incluir múltiples hojas de trabajo usando un objeto `ExcelWriter`.

```python
# Escribir DataFrame a Excel
df.to_excel('archivo_guardado.xlsx', index=False)

# Guardar en varias hojas
with pd.ExcelWriter('archivo_multiple.xlsx') as writer:
    df.to_excel(writer, sheet_name='Hoja1', index=False)
    df.to_excel(writer, sheet_name='Hoja2', index=False)
```

#### **Parámetros útiles de `read_excel()` y `to_excel()`**
- **`sheet_name`**: El nombre de la hoja o su índice en el archivo Excel (por defecto es la primera hoja).
- **`engine`**: Especifica el motor de lectura, por ejemplo, `openpyxl` para `.xlsx` y `xlrd` para `.xls`.

---

## 🔹 **JSON (`pd.read_json()`, `.to_json()`)**

El formato JSON es ampliamente utilizado para almacenar datos estructurados. Pandas ofrece métodos para convertir entre `DataFrame` y JSON.

### **Leer un archivo JSON**

Usamos **`pd.read_json()`** para leer datos en formato JSON y convertirlos en un `DataFrame`. JSON es particularmente útil para almacenar datos en estructuras jerárquicas.

```python
# Leer archivo JSON
df = pd.read_json('archivo.json')

# Mostrar las primeras filas
print(df.head())
```

### **Escribir un DataFrame a un archivo JSON**

Con **`.to_json()`**, puedes convertir un `DataFrame` en formato JSON. El parámetro **`orient`** define cómo se estructura el archivo JSON.

```python
# Escribir DataFrame a archivo JSON
df.to_json('archivo_guardado.json', orient='records', lines=True)
```

#### **Parámetros útiles de `read_json()` y `to_json()`**
- **`orient`**: Define cómo se estructuran los datos en el archivo JSON (por ejemplo, `records`, `split`, `index`, `columns`).
- **`lines`**: Si es `True`, cada línea es un objeto JSON en lugar de tener un solo objeto.

---

### **Resumen**

- **CSV**: Usa **`pd.read_csv()`** para leer y **`.to_csv()`** para escribir archivos CSV.
- **Excel**: Usa **`pd.read_excel()`** para leer y **`.to_excel()`** para escribir archivos Excel.
- **JSON**: Usa **`pd.read_json()`** para leer y **`.to_json()`** para escribir archivos JSON.
- Pandas ofrece parámetros adicionales que permiten personalizar la lectura y escritura, como `index_col`, `sep`, `sheet_name` y `orient`.

