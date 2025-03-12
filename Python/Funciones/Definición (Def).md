
Las funciones en Python son bloques de código reutilizables que realizan una tarea específica. Puedes definir funciones para organizar y simplificar tu código, hacer que sea más modular y reutilizable, y facilitar la depuración. Las funciones se definen utilizando la palabra clave `def`.

## Sintaxis básica

```python
def nombre_funcion(parametros):
    # Bloque de código
    return valor
```

### Detalles:
- `def` es la palabra clave para definir una función.
- `nombre_funcion` es el nombre de la función, que sigue las reglas de nomenclatura de Python (puede contener letras, números y guiones bajos, pero no puede empezar con un número).
- `parametros` son los valores que se pasan a la función para ser procesados. Pueden ser uno o varios.
- El bloque de código dentro de la función se ejecuta cada vez que se llama a la función.
- `return` es la instrucción que devuelve un valor desde la función, que luego puede ser utilizado fuera de ella. Si no se usa `return`, la función devolverá `None` por defecto.

### Ejemplo básico:

```python
def saludar():
    print("¡Hola, Mundo!")

saludar()  # Llama a la función y muestra "¡Hola, Mundo!"
```

En este caso, la función `saludar` no recibe ningún parámetro ni devuelve nada. Solo imprime un mensaje en la consola.

### Ejemplo con parámetros:

```python
def saludar(nombre):
    print(f"¡Hola, {nombre}!")

saludar("Juan")  # Llama a la función y muestra "¡Hola, Juan!"
saludar("Ana")   # Llama a la función y muestra "¡Hola, Ana!"
```

Aquí, la función `saludar` toma un parámetro llamado `nombre` y lo usa para imprimir un saludo personalizado.

### Ejemplo con retorno de valor:

```python
def sumar(a, b):
    return a + b

resultado = sumar(3, 4)  # 7
print(resultado)  # Muestra 7
```

La función `sumar` toma dos parámetros (`a` y `b`), los suma y devuelve el resultado con `return`.

## Parámetros por defecto

Es posible asignar valores por defecto a los parámetros de una función. Si no se pasa un argumento para esos parámetros cuando se llama a la función, se usará el valor por defecto.

### Ejemplo:

```python
def saludar(nombre="Mundo"):
    print(f"¡Hola, {nombre}!")

saludar()        # "¡Hola, Mundo!"
saludar("Juan")  # "¡Hola, Juan!"
```

En este caso, si no se pasa ningún valor a `nombre`, la función usará el valor `"Mundo"` por defecto.

### Ejemplo con múltiples parámetros por defecto:

```python
def crear_usuario(nombre="Invitado", edad=18):
    return f"Nombre: {nombre}, Edad: {edad}"

usuario = crear_usuario()               # "Nombre: Invitado, Edad: 18"
usuario2 = crear_usuario("Carlos")      # "Nombre: Carlos, Edad: 18"
usuario3 = crear_usuario("Ana", 25)     # "Nombre: Ana, Edad: 25"
```

## Parámetros arbitrarios: `*args` y `**kwargs`

En algunos casos, no sabemos cuántos argumentos se van a pasar a la función. Para estos casos, Python nos permite usar `*args` para una cantidad variable de argumentos posicionales, y `**kwargs` para una cantidad variable de argumentos con nombre.

### `*args` (Argumentos posicionales arbitrarios)

El uso de `*args` permite recibir un número indefinido de argumentos posicionales.

```python
def sumar_todos(*args):
    return sum(args)

resultado = sumar_todos(1, 2, 3, 4)  # 10
print(resultado)
```

En este ejemplo, `*args` permite pasar cualquier número de argumentos y sumarlos dentro de la función.

### `**kwargs` (Argumentos con nombre arbitrarios)

El uso de `**kwargs` permite recibir un número indefinido de argumentos que se pasan como un diccionario, es decir, con nombre.

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

Aquí, `**kwargs` permite recibir un número variable de argumentos con nombre y acceder a ellos como un diccionario.

### Combinando `*args` y `**kwargs`

Es posible usar tanto `*args` como `**kwargs` en una misma función.

```python
def ejemplo(*args, **kwargs):
    print("Argumentos posicionales:", args)
    print("Argumentos con nombre:", kwargs)

ejemplo(1, 2, 3, nombre="Juan", edad=25)
# Salida:
# Argumentos posicionales: (1, 2, 3)
# Argumentos con nombre: {'nombre': 'Juan', 'edad': 25}
```

## Funciones que retornan múltiples valores

Python permite devolver múltiples valores desde una función. Estos valores se devuelven como una tupla.

```python
def calcular(a, b):
    suma = a + b
    resta = a - b
    return suma, resta

resultado_suma, resultado_resta = calcular(10, 5)
print("Suma:", resultado_suma)  # 15
print("Resta:", resultado_resta)  # 5
```

La función `calcular` devuelve dos valores, que se asignan a dos variables al momento de llamarla.

## Funciones recursivas

Una función recursiva es aquella que se llama a sí misma. Esto se usa cuando una tarea se puede dividir en sub-tareas similares.

### Ejemplo:

```python
def factorial(n):
    if n == 1:
        return 1
    else:
        return n * factorial(n-1)

print(factorial(5))  # 120
```

En este ejemplo, la función `factorial` se llama a sí misma para calcular el factorial de un número.

## Resumen

- **Definición de funciones**: Usamos `def` para definir una función.
- **Parámetros**: Pueden ser posicionales, por defecto, arbitrarios (`*args`) o con nombre arbitrario (`**kwargs`).
- **Retorno de valores**: La función puede devolver valores usando `return`.
- **Funciones recursivas**: Funciones que se llaman a sí mismas.
- **Múltiples valores de retorno**: Una función puede devolver varios valores como una tupla.

