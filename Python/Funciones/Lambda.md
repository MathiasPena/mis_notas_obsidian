
Las **funciones lambda** son funciones anónimas, ligeras y compactas, definidas usando la palabra clave `lambda` en lugar de `def`. Son útiles cuando necesitas una función pequeña y no quieres escribir una definición completa de función.

## 3.1 Sintaxis Básica

La sintaxis básica de una función lambda es:

```python
lambda argumentos: expresión
```

- `argumentos`: Son los parámetros que recibe la función.
- `expresión`: Es el cálculo o retorno que realiza la función.

### Ejemplo:

```python
suma = lambda x, y: x + y
print(suma(3, 4))  # 7
```

En este caso, la función lambda toma dos parámetros (`x` y `y`), y devuelve su suma.

## 3.2 Funciones Lambda como Parámetros

Las funciones lambda son comúnmente usadas como argumentos de otras funciones, especialmente cuando se usa `map()`, `filter()` o `sorted()`.

### Ejemplo con `map()`:

```python
numeros = [1, 2, 3, 4, 5]
resultado = map(lambda x: x ** 2, numeros)  # Eleva cada número al cuadrado
print(list(resultado))  # [1, 4, 9, 16, 25]
```

En este caso, `map()` aplica la función lambda a cada elemento de la lista `numeros`.

### Ejemplo con `filter()`:

```python
numeros = [1, 2, 3, 4, 5, 6]
resultado = filter(lambda x: x % 2 == 0, numeros)  # Filtra los números pares
print(list(resultado))  # [2, 4, 6]
```

Aquí, `filter()` usa la lambda para filtrar los números pares.

### Ejemplo con `sorted()`:

```python
personas = [("Juan", 25), ("Ana", 30), ("Carlos", 20)]
personas_ordenadas = sorted(personas, key=lambda x: x[1])  # Ordena por edad
print(personas_ordenadas)  # [('Carlos', 20), ('Juan', 25), ('Ana', 30)]
```

En este caso, la lambda se utiliza para ordenar la lista de tuplas por el segundo elemento (la edad).

## 3.3 Funciones Lambda Multilínea

Aunque las funciones lambda son más conocidas por ser de una sola línea, también se pueden usar para definir funciones de múltiples líneas, aunque no es lo más común.

### Ejemplo:

```python
lambda x: (
    print(f"Recibiendo el valor {x}"), 
    x ** 2
)
```

Sin embargo, para funciones más complejas que requieren múltiples pasos, es mejor usar una función definida con `def`, ya que las funciones lambda están pensadas para ser simples y concisas.

## 3.4 Limitaciones de las Funciones Lambda

- **No pueden contener sentencias complejas**: Solo se puede usar una única expresión, no varias.
- **No son tan legibles en algunos casos**: Si la función es demasiado compleja, el uso de `def` es preferible para mejorar la legibilidad.

## 3.5 Comparación entre `lambda` y `def`

| Característica               | `lambda`                         | `def`                          |
|------------------------------|----------------------------------|--------------------------------|
| Sintaxis                     | `lambda argumentos: expresión`   | `def nombre_funcion():`        |
| Función anónima               | Sí                               | No                             |
| Puede tener múltiples expresiones | No                             | Sí                             |
| Más legible                   | No en funciones complejas       | Sí                             |

### Ejemplo comparativo:

```python
# Usando def
def suma(x, y):
    return x + y

# Usando lambda
suma_lambda = lambda x, y: x + y
```

Ambas funciones hacen lo mismo, pero la versión con `lambda` es más concisa.

## 3.6 Casos de Uso Comunes

1. **Funciones de orden superior**: Las funciones lambda se utilizan con funciones como `map()`, `filter()`, `sorted()`, `reduce()`, entre otras.
2. **Funciones pequeñas y simples**: Útiles cuando necesitas funciones rápidas y simples sin la necesidad de un nombre o una declaración completa.

## Resumen

- **Sintaxis**: `lambda argumentos: expresión`
- **Usos comunes**: `map()`, `filter()`, `sorted()`, y en general donde se necesite una función simple y rápida.
- **Ventajas**: Son concisas y fáciles de usar para funciones simples.
- **Limitaciones**: No son recomendables para funciones complejas o que requieran múltiples sentencias.

