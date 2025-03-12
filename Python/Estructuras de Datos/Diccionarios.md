# Diccionarios en Python

Los diccionarios son estructuras de datos que almacenan pares clave-valor.

## Creación de un Diccionario
```python
# Diccionario vacío
diccionario = {}
diccionario2 = dict()

# Diccionario con valores iniciales
diccionario = {"nombre": "Juan", "edad": 25, "ciudad": "Montevideo"}
```

## Acceder a Valores
```python
print(diccionario["nombre"])  # "Juan"
print(diccionario.get("edad"))  # 25
```

## Modificar Valores
```python
diccionario["edad"] = 30  # Cambia el valor de "edad"
```

## Agregar y Eliminar Elementos
```python
diccionario["pais"] = "Uruguay"  # Agregar un nuevo par clave-valor
del diccionario["ciudad"]  # Eliminar un elemento
valor_eliminado = diccionario.pop("pais")  # Eliminar y obtener el valor eliminado
```

## Iterar sobre un Diccionario
```python
# Iterar claves
for clave in diccionario:
    print(clave, diccionario[clave])

# Iterar valores
for valor in diccionario.values():
    print(valor)

# Iterar claves y valores
for clave, valor in diccionario.items():
    print(clave, ":", valor)
```

## Comprobar si una Clave Existe
```python
if "edad" in diccionario:
    print("La clave 'edad' existe en el diccionario")
```

## Métodos Útiles
```python
print(diccionario.keys())   # Obtener todas las claves
print(diccionario.values()) # Obtener todos los valores
print(diccionario.items())  # Obtener todos los pares clave-valor
```

## Copiar un Diccionario
```python
diccionario_copia = diccionario.copy()
```

## Fusionar Diccionarios
```python
otro_diccionario = {"altura": 175}
diccionario.update(otro_diccionario)  # Agrega claves de otro diccionario
```

## Eliminar Todos los Elementos
```python
diccionario.clear()
