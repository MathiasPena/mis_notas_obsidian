# 2. Lectura y Escritura de Archivos

Python permite leer y escribir archivos de texto de manera sencilla con la función `open()`. Es importante manejar los archivos correctamente para evitar errores y fugas de recursos.

---

## 1. Lectura de Archivos

Para leer un archivo, se usa el modo `'r'` (lectura). Hay varias formas de obtener el contenido:

### Leer todo el archivo con `.read()`
```python
with open("archivo.txt", "r") as archivo:
    contenido = archivo.read()
print(contenido)
```

> ⚠️ **Precaución:** `.read()` carga todo el contenido en memoria. No recomendable para archivos grandes.

### Leer línea por línea con `.readline()`
```python
with open("archivo.txt", "r") as archivo:
    linea = archivo.readline()  # Lee solo una línea
    print(linea)
```

### Leer todas las líneas con `.readlines()`
```python
with open("archivo.txt", "r") as archivo:
    lineas = archivo.readlines()  # Retorna una lista con todas las líneas
    for linea in lineas:
        print(linea.strip())  # Elimina saltos de línea al imprimir
```

### Leer línea por línea en un bucle (forma recomendada)
```python
with open("archivo.txt", "r") as archivo:
    for linea in archivo:
        print(linea.strip())
```
> ✅ **Ventaja:** No carga todo el archivo en memoria, útil para archivos grandes.

---

## 2. Escritura de Archivos

Para escribir en un archivo, se usa el modo `'w'` (escribir) o `'a'` (agregar).

### Sobrescribir archivo con `.write()` (`'w'`)
```python
with open("archivo.txt", "w") as archivo:
    archivo.write("Primera línea\n")
    archivo.write("Segunda línea\n")
```
> ⚠️ **Cuidado:** Si el archivo existe, su contenido será eliminado antes de escribir.

### Agregar contenido con `.write()` (`'a'`)
```python
with open("archivo.txt", "a") as archivo:
    archivo.write("Esta línea se agrega sin borrar las anteriores.\n")
```

### Escribir una lista de líneas con `.writelines()`
```python
lineas = ["Línea 1\n", "Línea 2\n", "Línea 3\n"]
with open("archivo.txt", "w") as archivo:
    archivo.writelines(lineas)  # Escribe todas las líneas de la lista
```

---

## 3. Lectura y Escritura Simultánea (`'r+'`, `'w+'`, `'a+'`)

Python permite abrir archivos para leer y escribir al mismo tiempo.

### Modo `'r+'` (lectura y escritura sin borrar contenido)
```python
with open("archivo.txt", "r+") as archivo:
    contenido = archivo.read()
    archivo.write("\nNueva línea agregada con 'r+'.")
```

### Modo `'w+'` (lectura y escritura, borra contenido)
```python
with open("archivo.txt", "w+") as archivo:
    archivo.write("Nuevo contenido con 'w+'.\n")  # Borra todo antes de escribir
    archivo.seek(0)  # Mueve el cursor al inicio para leer
    print(archivo.read())  # Leer el contenido después de escribir
```

### Modo `'a+'` (lectura y escritura sin borrar)
```python
with open("archivo.txt", "a+") as archivo:
    archivo.write("\nLínea agregada con 'a+'.")
    archivo.seek(0)  # Mueve el cursor al inicio
    print(archivo.read())  # Leer todo el contenido
```

---

## 4. Manejo de Archivos Binarios

Para trabajar con archivos no de texto (imágenes, audio, PDFs), se usan los modos `'rb'`, `'wb'`, `'ab'`.

### Leer un archivo binario (`'rb'`)
```python
with open("imagen.jpg", "rb") as archivo:
    datos = archivo.read()  # Lee los bytes del archivo
```

### Escribir un archivo binario (`'wb'`)
```python
with open("copia.jpg", "wb") as archivo:
    archivo.write(datos)  # Guarda los bytes en otro archivo
```

---

## 5. Eliminar un Archivo

Para eliminar archivos en Python se usa el módulo `os`:

```python
import os
os.remove("archivo.txt")
```
> ⚠️ **Precaución:** No hay confirmación antes de eliminar el archivo.

---

## 6. Resumen Rápido
| Modo  | Descripción |
|--------|--------------------------------------------|
| `'r'`  | Lectura (error si el archivo no existe). |
| `'w'`  | Escritura (borra el contenido existente). |
| `'a'`  | Agregar al final del archivo. |
| `'r+'` | Lectura y escritura sin borrar contenido. |
| `'w+'` | Lectura y escritura, borra el archivo antes. |
| `'a+'` | Lectura y escritura, no borra contenido. |
| `'rb'` | Lectura en binario. |
| `'wb'` | Escritura en binario. |
| `'ab'` | Agregar en binario. |

