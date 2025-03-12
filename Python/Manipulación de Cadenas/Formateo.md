
Python ofrece varias formas de formatear cadenas. Las más comunes son las **f-strings**, el método `.format()` y el operador `%`. A continuación se explican estas tres opciones.

## 2.1 **f-strings** (Literales de Cadenas Formateadas)

Introducidas en Python 3.6, las f-strings son la forma más moderna y recomendada de formatear cadenas. Permiten insertar expresiones dentro de cadenas utilizando llaves `{}` y precediendo la cadena con una `f`.

### Sintaxis:
```python
f"Texto {expresión} más texto"
```

- **expresión**: Puede ser cualquier expresión válida, como variables o cálculos.

### Ejemplo:

```python
nombre = "Juan"
edad = 25
texto = f"Mi nombre es {nombre} y tengo {edad} años."
print(texto)  # "Mi nombre es Juan y tengo 25 años."
```

Las f-strings también permiten formatear números, fechas, y más.

### Ejemplo con formateo de números:

```python
precio = 9.99
texto = f"El precio es: {precio:.2f}"
print(texto)  # "El precio es: 9.99"
```

En este ejemplo, `.2f` formatea el número a 2 decimales.

### Ejemplo con expresiones:

```python
x = 10
texto = f"El doble de {x} es {x*2}."
print(texto)  # "El doble de 10 es 20."
```

## 2.2 **`.format()`**

El método `.format()` es otra forma de formatear cadenas y es compatible con versiones de Python anteriores a la 3.6. Este método permite insertar variables y valores en una cadena mediante índices o nombres.

### Sintaxis:
```python
"Texto {} más texto".format(valor)
```

También puedes usar índices y nombres para mayor claridad.

### Ejemplo básico:

```python
nombre = "Juan"
edad = 25
texto = "Mi nombre es {} y tengo {} años.".format(nombre, edad)
print(texto)  # "Mi nombre es Juan y tengo 25 años."
```

### Ejemplo con índices:

```python
texto = "El {0} es {1} y el {0} es {2}.".format("sol", "brillante", "caliente")
print(texto)  # "El sol es brillante y el sol es caliente."
```

### Ejemplo con nombres de parámetros:

```python
texto = "Mi nombre es {nombre} y tengo {edad} años.".format(nombre="Juan", edad=25)
print(texto)  # "Mi nombre es Juan y tengo 25 años."
```

## 2.3 **Operador `%`**

El operador `%` es un método más antiguo y menos flexible de formatear cadenas, pero aún es útil en versiones anteriores a Python 3.6. Este método utiliza un estilo similar al de C para formatear cadenas.

### Sintaxis:
```python
"Texto % (valor)"
```

O para múltiples valores:

```python
"Texto % (valor1, valor2)"
```

### Ejemplo básico:

```python
nombre = "Juan"
edad = 25
texto = "Mi nombre es %s y tengo %d años." % (nombre, edad)
print(texto)  # "Mi nombre es Juan y tengo 25 años."
```

### Ejemplo con múltiples valores:

```python
texto = "El %s es %s y el %s es %s." % ("sol", "brillante", "cielo", "azul")
print(texto)  # "El sol es brillante y el cielo es azul."
```

### Formateo de números:

```python
precio = 9.99
texto = "El precio es: %.2f" % precio
print(texto)  # "El precio es: 9.99"
```

## 2.4 Comparativa y Recomendaciones

### Comparativa entre los métodos:

| Método        | Ventajas                                      | Desventajas                                 |
|---------------|-----------------------------------------------|---------------------------------------------|
| **f-strings** | Sintaxis clara, eficiente y moderna. Soporta expresiones dentro de la cadena. | Solo disponible en Python 3.6 y versiones posteriores. |
| **`.format()`** | Compatible con versiones anteriores, flexible. | Menos intuitivo y más verboso que las f-strings. |
| **`%`**        | Rápido y compatible con versiones antiguas de Python. | Sintaxis más antigua y menos flexible. |

### Recomendación:

- Usar **f-strings** si estás trabajando con Python 3.6 o versiones posteriores, ya que son más legibles y eficientes.
- Usar **`.format()`** si necesitas compatibilidad con versiones de Python anteriores a 3.6.
- El operador **`%`** es útil principalmente si trabajas con código legado.

## Resumen

- **f-strings**: Formato moderno, eficiente y fácil de usar, ideal para Python 3.6+.
- **`.format()`**: Método flexible, compatible con versiones anteriores.
- **Operador `%`**: Método más antiguo, útil en situaciones de compatibilidad retroactiva.

