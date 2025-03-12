
Las **comprehensions** permiten crear nuevas colecciones de manera concisa y eficiente.

## 1. List Comprehension

Crea listas a partir de otras secuencias o rangos.

### Sintaxis:

```python
[nueva_variable for item in secuencia if condicion]
```

### Ejemplo:

```python
# Crear una lista con los cuadrados de los números del 0 al 4
cuadrados = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
```

## 2. Dictionary Comprehension

Crea diccionarios de manera compacta.

### Sintaxis:

```python
{clave: valor for item in secuencia if condicion}
```

### Ejemplo:

```python
# Crear un diccionario con números y sus cuadrados
cuadrados_dict = {x: x**2 for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## 3. Set Comprehension

Crea sets eliminando duplicados de manera directa.

### Sintaxis:

```python
{item for item in secuencia if condicion}
```

### Ejemplo:

```python
# Crear un set con los cuadrados de los números del 0 al 4 (sin duplicados)
cuadrados_set = {x**2 for x in range(5)}  # {0, 1, 4, 9, 16}
```

## 4. Nested Comprehensions

Comprehensions dentro de comprehensions.

### Ejemplo:

```python
# Crear una lista de listas con los cuadrados de los números
matriz = [[x**2 for x in range(3)] for _ in range(3)]  # [[0, 1, 4], [0, 1, 4], [0, 1, 4]]
```

## Resumen

- **List Comprehension:** `[expresion for item in secuencia if condicion]`
- **Dict Comprehension:** `{clave: valor for item in secuencia if condicion}`
- **Set Comprehension:** `{expresion for item in secuencia if condicion}`
- **Nested Comprehensions:** Comprehensions dentro de comprehensions para crear estructuras más complejas.
