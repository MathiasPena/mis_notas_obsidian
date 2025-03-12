
El módulo `os` proporciona una manera de interactuar con el **sistema operativo** desde Python. Permite acceder a funciones como la manipulación de archivos, el manejo de variables de entorno y la interacción con rutas de archivos.

---

## 🔹 ¿Qué es `os`?

El módulo `os` permite trabajar con el sistema operativo en el que se está ejecutando Python. Es útil para interactuar con el sistema de archivos, gestionar procesos, manipular rutas y trabajar con variables de entorno.

---

## 🔹 `os.environ` - Variables de Entorno

`os.environ` es un diccionario que contiene las **variables de entorno** del sistema operativo. Puedes acceder a variables como el **PATH**, configuraciones del sistema, y otras configuraciones de entorno necesarias para ejecutar programas.

### 🛠️ Ejemplo: Uso de `os.environ`

```python
import os

# Acceder a una variable de entorno
print(os.environ.get('HOME'))  # Imprime el directorio HOME en sistemas Unix

# Establecer una nueva variable de entorno
os.environ['MY_VAR'] = 'valor'
print(os.environ['MY_VAR'])  # valor
```

📌 **Explicación:**
- `os.environ.get('HOME')` accede a la variable de entorno `HOME`.
- `os.environ['MY_VAR'] = 'valor'` permite establecer nuevas variables de entorno, aunque solo durarán mientras el script se ejecute.

---

## 🔹 `os.path` - Manipulación de Rutas de Archivos

El submódulo `os.path` permite trabajar con **rutas de archivos y directorios** de manera independiente del sistema operativo. Proporciona funciones para construir, analizar y manipular rutas de forma eficiente.

### 🛠️ Ejemplo: Uso de `os.path`

```python
import os

# Obtener el nombre base de un archivo
ruta = "/home/user/archivo.txt"
print(os.path.basename(ruta))  # archivo.txt

# Obtener el directorio de un archivo
print(os.path.dirname(ruta))  # /home/user

# Verificar si un archivo existe
print(os.path.exists(ruta))  # True o False

# Unir directorios y archivos
ruta_unida = os.path.join("/home/user", "archivo.txt")
print(ruta_unida)  # /home/user/archivo.txt

# Verificar si una ruta es un archivo o directorio
print(os.path.isfile(ruta))  # True o False
print(os.path.isdir(ruta))  # True o False
```

📌 **Explicación:**
- `os.path.basename(ruta)` devuelve el nombre del archivo de una ruta.
- `os.path.dirname(ruta)` devuelve el directorio de la ruta.
- `os.path.exists(ruta)` verifica si la ruta existe.
- `os.path.join()` es útil para combinar rutas de forma correcta, independientemente del sistema operativo.

---

## 🔹 Otras Funciones Útiles de `os`

1. **`os.getcwd()`**: Obtiene el directorio de trabajo actual.
   
   ```python
   import os
   print(os.getcwd())  # Imprime el directorio actual
   ```

2. **`os.chdir(path)`**: Cambia el directorio de trabajo actual.
   
   ```python
   import os
   os.chdir('/ruta/a/mi/directorio')  # Cambia al directorio especificado
   ```

3. **`os.mkdir(path)`**: Crea un nuevo directorio.
   
   ```python
   import os
   os.mkdir('/ruta/a/nuevo_directorio')  # Crea un directorio
   ```

4. **`os.remove(path)`**: Elimina un archivo.
   
   ```python
   import os
   os.remove('/ruta/a/mi/archivo.txt')  # Elimina el archivo
   ```

5. **`os.rmdir(path)`**: Elimina un directorio vacío.
   
   ```python
   import os
   os.rmdir('/ruta/a/directorio')  # Elimina un directorio vacío
   ```

---

## 🚀 Conclusión

- El módulo `os` es esencial para interactuar con el sistema operativo, permitiendo manejar archivos, directorios y variables de entorno de manera eficiente.
- **`os.environ`** te permite trabajar con las variables de entorno del sistema operativo, mientras que **`os.path`** facilita la manipulación de rutas de archivos y directorios.
- Utiliza estas herramientas para gestionar archivos, directorios y configuraciones del sistema operativo en tus programas Python.

📌 **Usar `os` te permitirá hacer que tus scripts interactúen de manera eficiente con el sistema operativo, mejorando la flexibilidad y la capacidad de tus programas.**
