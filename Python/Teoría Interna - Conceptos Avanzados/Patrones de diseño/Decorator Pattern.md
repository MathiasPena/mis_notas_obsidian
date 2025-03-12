
### Decorator Pattern (`@wraps` y `functools`)

El **Decorator Pattern** es un patrón de diseño estructural que permite añadir funcionalidades a una función u objeto sin modificar su estructura original. En Python, los decoradores se implementan usando **funciones de orden superior** y la sintaxis especial con `@`.

Para mantener los metadatos originales de las funciones decoradas (nombre, docstring, etc.), se usa `functools.wraps`, lo cual evita problemas con introspección y debugging.

---

## Implementación de un decorador básico

```python
def mi_decorador(func):
    def wrapper(*args, **kwargs):
        print("Antes de ejecutar la función")
        resultado = func(*args, **kwargs)
        print("Después de ejecutar la función")
        return resultado
    return wrapper

@mi_decorador
def saludar():
    print("¡Hola, mundo!")

saludar()
```

**Salida:**
```
Antes de ejecutar la función
¡Hola, mundo!
Después de ejecutar la función
```

Aquí `mi_decorador` envuelve la función `saludar`, ejecutando código antes y después de su ejecución.

---

## Uso de `functools.wraps` para mantener metadatos

Sin `@wraps`, los decoradores pueden sobrescribir el nombre y la documentación de la función original. Para evitar esto, se usa `functools.wraps`:

```python
import functools

def mi_decorador(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print("Ejecutando decorador...")
        return func(*args, **kwargs)
    return wrapper

@mi_decorador
def funcion_ejemplo():
    """Esta es una función de ejemplo."""
    print("Función ejecutada.")

print(funcion_ejemplo.__name__)  # Output: funcion_ejemplo
print(funcion_ejemplo.__doc__)   # Output: Esta es una función de ejemplo.
```

Sin `@wraps`, `funcion_ejemplo.__name__` mostraría `wrapper` en lugar de `funcion_ejemplo`.

---

## Decorador con parámetros

Los decoradores también pueden aceptar argumentos envolviendo el decorador dentro de otra función:

```python
def repetir(n):
    def decorador(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(n):
                func(*args, **kwargs)
        return wrapper
    return decorador

@repetir(3)
def decir_hola():
    print("Hola!")

decir_hola()
```

**Salida:**
```
Hola!
Hola!
Hola!
```

Aquí `@repetir(3)` repite la ejecución de la función `decir_hola` tres veces.

---

## Aplicaciones del Decorator Pattern

✅ **Logging**: Añadir logs a funciones sin modificar su código.  
✅ **Autenticación**: Verificar permisos antes de ejecutar ciertas funciones.  
✅ **Medición de rendimiento**: Calcular el tiempo de ejecución de funciones.  
✅ **Caching**: Usar `functools.lru_cache` para almacenar resultados de funciones costosas.  

Ejemplo de **decorador para medir tiempo de ejecución**:

```python
import time

def medir_tiempo(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        inicio = time.time()
        resultado = func(*args, **kwargs)
        fin = time.time()
        print(f"Tiempo de ejecución: {fin - inicio:.4f} segundos")
        return resultado
    return wrapper

@medir_tiempo
def operacion_pesada():
    time.sleep(2)
    print("Operación completada.")

operacion_pesada()
```

**Salida:**
```
Operación completada.
Tiempo de ejecución: 2.0001 segundos
```

---

## Resumen

El **Decorator Pattern** permite extender funcionalidades de manera limpia y reutilizable sin modificar el código original.  
`functools.wraps` es clave para mantener metadatos de funciones decoradas.  
Los decoradores son muy usados en Python para logging, autenticación, caching y medición de rendimiento.
