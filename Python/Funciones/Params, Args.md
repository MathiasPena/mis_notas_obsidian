
En Python, los parámetros son las variables que se definen en la firma de la función, y los argumentos son los valores que se pasan a esas funciones cuando se llaman. A continuación, se explican los diferentes tipos de parámetros que puedes usar al definir una función.

## 2.1 Parámetros Posicionales

Los **parámetros posicionales** son aquellos que se pasan a la función en el orden en que se definen. Deben ser proporcionados en el mismo orden que se encuentran en la firma de la función.

### Ejemplo:

```python
def saludar(nombre, edad):
    print(f"Hola {nombre}, tienes {edad} años.")

saludar("Juan", 25)  # Llamada correcta
# Salida: "Hola Juan, tienes 25 años."
```

En este caso, `nombre` y `edad` son parámetros posicionales. Es importante pasar los argumentos en el mismo orden en que están definidos en la función.

## 2.2 Parámetros con Valores Predeterminados

Puedes asignar valores predeterminados a los parámetros. Si no se pasa un argumento para esos parámetros, se utilizarán los valores por defecto.

### Ejemplo:

```python
def saludar(nombre="Mundo", edad=18):
    print(f"Hola {nombre}, tienes {edad} años.")

saludar()          # "Hola Mundo, tienes 18 años."
saludar("Carlos")  # "Hola Carlos, tienes 18 años."
saludar("Ana", 30) # "Hola Ana, tienes 30 años."
```

En este caso, si no se proporciona un valor para `nombre` o `edad`, se utilizarán `"Mundo"` y `18` respectivamente.

## 2.3 Parámetros Arbitrarios con `*args`

A veces no sabemos cuántos argumentos se van a pasar a la función. El uso de `*args` permite a la función aceptar un número variable de argumentos posicionales. Los argumentos pasados a través de `*args` se almacenan como una tupla.

### Ejemplo:

```python
def sumar_todos(*args):
    return sum(args)

print(sumar_todos(1, 2, 3))  # 6
print(sumar_todos(10, 20))   # 30
```

Aquí, `*args` permite que la función acepte cualquier número de argumentos posicionales.

### Otro Ejemplo con Iteración:

```python
def mostrar_nombres(*args):
    for nombre in args:
        print(f"Nombre: {nombre}")

mostrar_nombres("Juan", "Ana", "Carlos")  # Imprime los nombres uno por uno
```

## 2.4 Parámetros con Nombre Arbitrario con `**kwargs`

El uso de `**kwargs` permite que la función reciba un número variable de argumentos, pero con nombre. Los argumentos se pasan como un diccionario, donde las claves son los nombres de los parámetros y los valores son los valores asociados a esos parámetros.

### Ejemplo:

```python
def mostrar_datos(**kwargs):
    for clave, valor in kwargs.items():
        print(f"{clave}: {valor}")

mostrar_datos(nombre="Juan", edad=30, profesion="Ingeniero")
# Salida:
# nombre: Juan
# edad: 30
# profesion: Ingeniero
```

En este caso, `**kwargs` captura todos los argumentos con nombre y los convierte en un diccionario.

### Otro Ejemplo con Condiciones:

```python
def mostrar_info(**kwargs):
    if "edad" in kwargs:
        print(f"Edad: {kwargs['edad']}")
    else:
        print("Edad no proporcionada.")

mostrar_info(nombre="Carlos", edad=35)  # "Edad: 35"
mostrar_info(nombre="Ana")                # "Edad no proporcionada."
```

## 2.5 Combinando Parámetros Posicionales, `*args` y `**kwargs`

Puedes combinar parámetros posicionales, `*args` y `**kwargs` en una sola función. La clave es que los parámetros posicionales deben ir primero, luego `*args`, y finalmente `**kwargs`.

### Ejemplo:

```python
def funcion_completa(param1, param2, *args, **kwargs):
    print(f"Parametro 1: {param1}")
    print(f"Parametro 2: {param2}")
    print(f"Argumentos adicionales: {args}")
    print(f"Argumentos con nombre: {kwargs}")

funcion_completa(10, 20, 30, 40, nombre="Juan", edad=30)
# Salida:
# Parametro 1: 10
# Parametro 2: 20
# Argumentos adicionales: (30, 40)
# Argumentos con nombre: {'nombre': 'Juan', 'edad': 30}
```

En este caso, `param1` y `param2` son parámetros posicionales, `*args` captura los argumentos adicionales, y `**kwargs` captura los argumentos con nombre.

## 2.6 Argumentos de Tipo Posicional con `*` y `**`

En Python 3.8+, puedes usar `*` para indicar que todos los parámetros a la derecha de él deben ser pasados como argumentos de palabra clave (nombrados). Del mismo modo, puedes usar `**` para hacer que todos los argumentos de una función sean de palabra clave.

### Ejemplo con `*`:

```python
def funcion_posicional(*, nombre, edad):
    print(f"Nombre: {nombre}, Edad: {edad}")

funcion_posicional(nombre="Juan", edad=25)  # Correcto
# funcion_posicional("Juan", 25)  # Error: Argumentos deben ser nombrados
```

Aquí, `*` obliga a que todos los parámetros sean nombrados explícitamente.

### Ejemplo con `**`:

```python
def funcion_keyword(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

funcion_keyword(nombre="Ana", edad=28)  # nombre: Ana, edad: 28
```

## 2.7 Desempaquetado de Argumentos

Puedes desempaquetar los valores de un diccionario o una lista para pasarlos como argumentos a una función. Esto se hace con el operador `*` para listas o tuplas y `**` para diccionarios.

### Desempaquetado con `*`:

```python
def suma(a, b, c):
    return a + b + c

valores = [1, 2, 3]
print(suma(*valores))  # 6
```

### Desempaquetado con `**`:

```python
def mostrar_datos(nombre, edad):
    print(f"Nombre: {nombre}, Edad: {edad}")

info = {"nombre": "Juan", "edad": 30}
mostrar_datos(**info)  # Nombre: Juan, Edad: 30
```

## Resumen

- **Parámetros posicionales**: Se pasan en el orden en que se definen.
- **Parámetros por defecto**: Valores predeterminados que se usan si no se pasa un argumento.
- **`*args`**: Permite pasar un número variable de argumentos posicionales.
- **`**kwargs`**: Permite pasar un número variable de argumentos con nombre.
- **Combinación**: Puedes usar parámetros posicionales, `*args` y `**kwargs` juntos.
- **Desempaquetado**: Usando `*` para listas/tuplas y `**` para diccionarios, puedes desempaquetar valores y pasarlos como argumentos a la función.

