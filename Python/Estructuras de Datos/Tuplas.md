
## Definición

Una **tupla** es una estructura de datos inmutable en Python que puede contener diferentes tipos de datos.

```python
mi_tupla = (1, 2, 3, "hola", True)
```

## Características

- **Inmutables**: No pueden modificarse después de su creación.
- **Pueden contener cualquier tipo de datos**.
- **Se pueden anidar** (tuplas dentro de tuplas).
- **Admiten indexación y slicing**.

## Creación de Tuplas

### Tupla vacía

```python
mi_tupla = ()
```

### Tupla con elementos

```python
mi_tupla = (1, 2, 3)
```

### Tupla sin paréntesis (packing)

```python
mi_tupla = 1, 2, 3
```

### Tupla de un solo elemento (con coma)

```python
mi_tupla = (5,)
```

## Acceder a elementos

```python
tupla = (10, 20, 30)
print(tupla[0])  # 10
print(tupla[-1]) # 30
```

## Slicing

```python
tupla = (0, 1, 2, 3, 4, 5)
print(tupla[1:4])  # (1, 2, 3)
print(tupla[:3])   # (0, 1, 2)
print(tupla[::2])  # (0, 2, 4)
```

## Desempaquetado

```python
tupla = ("Python", 3.10, "Guido")
nombre, version, creador = tupla
print(nombre)  # Python
```

## Operaciones con Tuplas

### Concatenación

```python
tupla1 = (1, 2, 3)
tupla2 = (4, 5, 6)
tupla3 = tupla1 + tupla2
print(tupla3)  # (1, 2, 3, 4, 5, 6)
```

### Repetición

```python
tupla = ("Hola",) * 3
print(tupla)  # ('Hola', 'Hola', 'Hola')
```

## Métodos de Tuplas

|Método|Descripción|
|---|---|
|`count(x)`|Cuenta cuántas veces aparece `x` en la tupla.|
|`index(x)`|Devuelve el índice de la primera aparición de `x`.|

```python
tupla = (1, 2, 3, 2, 4, 2)
print(tupla.count(2))  # 3
print(tupla.index(3))  # 2
```

## Conversión entre listas y tuplas

```python
lista = [1, 2, 3]
tupla = tuple(lista)
print(tupla)  # (1, 2, 3)

nueva_lista = list(tupla)
print(nueva_lista)  # [1, 2, 3]
```

## Uso de Tuplas en Retorno de Funciones

```python
def coordenadas():
    return (10, 20)

x, y = coordenadas()
print(x, y)  # 10 20
```

## Cuándo Usar Tuplas en Lugar de Listas

- Cuando los datos no deben modificarse.
- Para mejorar el rendimiento (las tuplas son más rápidas y consumen menos memoria).
- Para claves en diccionarios (las tuplas son **hashables**, las listas no).

```python
diccionario = { (1, 2): "valor" }
print(diccionario[(1, 2)])  # "valor"
```