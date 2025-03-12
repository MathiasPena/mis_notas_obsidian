

El manejo de errores en Python se realiza utilizando las declaraciones `try`, `except`, y `finally`. Estas permiten manejar excepciones de manera controlada, evitar que el programa se detenga abruptamente y limpiar recursos cuando sea necesario.

## 4.1 Estructura Básica

La estructura básica de un bloque `try-except` es la siguiente:

```python
try:
    # Código que puede generar una excepción
except ExceptionType as e:
    # Código para manejar la excepción
```

- **`try`**: Contiene el código que puede generar una excepción.
- **`except`**: Captura la excepción especificada y permite manejarla.

### Ejemplo:

```python
try:
    x = 10 / 0  # Intentar dividir por cero
except ZeroDivisionError as e:
    print("Error: No se puede dividir por cero.")
```

En este caso, se produce una excepción `ZeroDivisionError`, que es capturada por el bloque `except`, y se imprime el mensaje correspondiente.

## 4.2 Manejo de Diferentes Excepciones

Puedes manejar diferentes tipos de excepciones utilizando múltiples bloques `except`.

### Ejemplo:

```python
try:
    num = int(input("Ingresa un número: "))
    resultado = 10 / num
except ValueError as e:
    print("Error: No es un número válido.")
except ZeroDivisionError as e:
    print("Error: No se puede dividir por cero.")
```

Aquí, se manejan tanto `ValueError` (si el usuario ingresa algo que no es un número) como `ZeroDivisionError` (si el número ingresado es cero).

## 4.3 Captura de Excepciones Generales

Si no sabes qué tipo de error puede ocurrir, puedes capturar todas las excepciones usando `except` sin especificar el tipo.

### Ejemplo:

```python
try:
    # Código que puede generar cualquier tipo de error
    x = int(input("Ingresa un número: "))
except Exception as e:
    print(f"Se ha producido un error: {e}")
```

Aunque esta forma es útil, no es recomendable capturar todas las excepciones de manera general en la mayoría de los casos, ya que oculta detalles importantes sobre el error.

## 4.4 Usando `else` con `try-except`

Puedes usar un bloque `else` para ejecutar código si no ocurre ninguna excepción en el bloque `try`.

### Ejemplo:

```python
try:
    num = int(input("Ingresa un número: "))
    resultado = 10 / num
except ZeroDivisionError:
    print("Error: No se puede dividir por cero.")
else:
    print(f"El resultado es: {resultado}")
```

Si no ocurre ningún error en el bloque `try`, el código dentro del bloque `else` se ejecutará.

## 4.5 Bloque `finally`

El bloque `finally` siempre se ejecuta, sin importar si ocurre una excepción o no. Es útil para liberar recursos como archivos o conexiones a bases de datos.

### Ejemplo:

```python
try:
    archivo = open("archivo.txt", "r")
    # Realizar operaciones con el archivo
except FileNotFoundError:
    print("Error: El archivo no existe.")
finally:
    print("El bloque finally se ejecuta siempre.")
    # Cerrar el archivo si fue abierto
    if 'archivo' in locals():
        archivo.close()
```

En este ejemplo, el bloque `finally` se asegura de que se cierre el archivo, independientemente de si ocurrió un error o no.

## 4.6 Excepciones Personalizadas

Puedes definir tus propias excepciones utilizando clases que heredan de `Exception`.

### Ejemplo:

```python
class MiError(Exception):
    pass

try:
    raise MiError("Algo salió mal")
except MiError as e:
    print(f"Excepción personalizada: {e}")
```

En este caso, se lanza una excepción personalizada `MiError`, que es capturada en el bloque `except`.

## 4.7 Resumen de la Estructura

1. **`try`**: Contiene el código que puede generar una excepción.
2. **`except`**: Captura y maneja la excepción.
3. **`else`**: (Opcional) Se ejecuta si no ocurre ninguna excepción en el bloque `try`.
4. **`finally`**: (Opcional) Se ejecuta siempre, independientemente de si ocurrió una excepción, ideal para la limpieza de recursos.

## Resumen

- **`try-except`**: Captura y maneja excepciones.
- **`else`**: Ejecuta código cuando no hay excepciones.
- **`finally`**: Ejecuta código de limpieza, sin importar si hubo excepciones o no.
- **Excepciones personalizadas**: Puedes crear tus propias excepciones para manejar errores específicos.

