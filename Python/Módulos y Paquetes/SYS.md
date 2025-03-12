

El módulo `sys` proporciona acceso a funciones y variables que interactúan con el **intérprete de Python** y el **entorno de ejecución**. Es útil para gestionar aspectos del entorno de ejecución, como argumentos de línea de comandos y rutas de búsqueda de módulos.

---

## 🔹 ¿Qué es `sys`?

`sys` es un módulo estándar que permite interactuar con el intérprete de Python y proporciona herramientas para acceder a variables y funciones que influyen en el funcionamiento del programa. Algunas de sus funcionalidades más comunes son el manejo de argumentos de línea de comandos y la manipulación de rutas de módulos.

---

## 🔹 `sys.argv` - Argumentos de Línea de Comandos

`sys.argv` es una lista que contiene los **argumentos pasados al script** de Python desde la línea de comandos. El primer elemento de la lista es siempre el nombre del script, y los siguientes son los argumentos proporcionados.

### 🛠️ Ejemplo: Uso de `sys.argv`

```python
import sys

# Si el script se ejecuta con los argumentos: python script.py arg1 arg2
print("Nombre del script:", sys.argv[0])  # script.py
print("Primer argumento:", sys.argv[1])   # arg1
print("Segundo argumento:", sys.argv[2])  # arg2
```

📌 **Explicación:**
- `sys.argv[0]` es el nombre del script.
- `sys.argv[1:]` contiene los argumentos adicionales pasados al script.

---

## 🔹 `sys.path` - Rutas de Búsqueda de Módulos

`sys.path` es una lista que contiene las rutas de búsqueda de módulos. Cuando importas un módulo, Python busca en las rutas especificadas en `sys.path`. Puedes modificar esta lista para incluir directorios adicionales si deseas cargar módulos desde ubicaciones personalizadas.

### 🛠️ Ejemplo: Uso de `sys.path`

```python
import sys

# Imprimir las rutas de búsqueda de módulos
print(sys.path)

# Agregar una nueva ruta al final
sys.path.append('/ruta/a/mis/modulos')

# Verificar si la nueva ruta fue añadida
print(sys.path)
```

📌 **Explicación:**
- `sys.path` incluye rutas predeterminadas, como el directorio donde está el script y las rutas de instalación de Python.
- Usar `sys.path.append('/ruta/a/mis/modulos')` permite añadir directorios personalizados para cargar módulos desde allí.

---

## 🔹 Otras Funciones de `sys`

1. **`sys.exit()`**: Termina el programa de forma inmediata. Puede aceptar un código de salida como argumento.
   
   ```python
   import sys
   sys.exit("Error: terminando el programa")
   ```

2. **`sys.version`**: Muestra la versión actual del intérprete de Python.
   
   ```python
   import sys
   print(sys.version)  # Ejemplo: 3.8.5 (default, Jul 20 2020, 12:00:00)
   ```

3. **`sys.platform`**: Muestra el nombre del sistema operativo en el que está corriendo Python.
   
   ```python
   import sys
   print(sys.platform)  # Ejemplo: 'win32' en Windows, 'darwin' en macOS
   ```

---

## 🚀 Conclusión

- El módulo `sys` es esencial para interactuar con el entorno de ejecución de Python, permitiendo manipular la búsqueda de módulos, manejar los argumentos de línea de comandos y controlar el comportamiento del intérprete.
- **`sys.argv`** es útil para capturar argumentos de la línea de comandos, y **`sys.path`** te permite modificar las rutas de búsqueda de módulos.
- Usar `sys` te ayuda a mejorar la flexibilidad y personalización de tus programas Python.

📌 **Usar `sys` eficientemente te permitirá controlar el entorno de ejecución y manejar de manera más efectiva la carga de módulos y los argumentos proporcionados en la ejecución.**
