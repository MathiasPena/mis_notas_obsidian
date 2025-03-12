# Bucles en Python

Los bucles permiten repetir un bloque de código. Existen dos tipos: `for` y `while`.

## 1. Bucle `for`

Itera sobre secuencias (listas, tuplas, cadenas, etc.).

### Sintaxis:

```python
for variable in secuencia:
    # Bloque de código
```

### Ejemplo con lista:

```python
frutas = ['manzana', 'banana', 'cereza']
for fruta in frutas:
    print(fruta)
```

### `range()`

Genera una secuencia de números.

```python
for i in range(5):  # Imprime 0, 1, 2, 3, 4
    print(i)
```

### `enumerate()`

Devuelve índice y valor.

```python
for index, fruta in enumerate(['manzana', 'banana']):
    print(index, fruta)  # 0 manzana, 1 banana
```

## 2. Bucle `while`

Ejecuta un bloque de código mientras se cumpla una condición.

### Sintaxis:

```python
while condicion:
    # Bloque de código
```

### Ejemplo:

```python
contador = 0
while contador < 5:  # Imprime 0, 1, 2, 3, 4
    print(contador)
    contador += 1
```

## 3. Sentencias dentro de los bucles

### `break`

Rompe el bucle.

```python
for i in range(10):
    if i == 5: break  # Salta cuando i == 5
```

### `continue`

Salta la iteración actual.

```python
for i in range(5):
    if i == 3: continue  # Salta cuando i == 3
```

### `else` con bucles

Se ejecuta si el bucle no fue interrumpido por `break`.

```python
for i in range(3):  # Imprime 0, 1, 2
    print(i)
else:
    print("Fin")  # Se ejecuta porque no hubo break
```

## Resumen

- **`for`:** Para iterar sobre secuencias.
- **`while`:** Ejecuta mientras se cumpla la condición.
- **`break`:** Sale del bucle.
- **`continue`:** Salta la iteración.
- **`else`:** Se ejecuta si no se interrumpe con `break`.

