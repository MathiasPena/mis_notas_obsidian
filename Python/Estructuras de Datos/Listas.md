
### 1. Creación de listas

```python
# Lista vacía
lista_vacia = []  

# Lista con elementos
lista_numeros = [1, 2, 3, 4, 5]  
lista_mixta = [1, "texto", 3.14, True]  
```

### 2. Acceder a elementos

```python
lista = [10, 20, 30, 40]
print(lista[0])  # Primer elemento -> 10
print(lista[-1]) # Último elemento -> 40
print(lista[1:3]) # Sublista -> [20, 30]
```

### 3. Modificar elementos

```python
lista[1] = 99  # Cambia el segundo elemento
lista.append(50)  # Agrega al final
lista.insert(2, 15)  # Inserta en índice 2
```

### 4. Eliminar elementos

```python
lista.remove(99)  # Elimina el primer 99 encontrado
valor = lista.pop(1)  # Elimina el índice 1 y lo devuelve
del lista[0]  # Elimina el primer elemento
lista.clear()  # Vacía la lista
```

### 5. Recorrer una lista

```python
# Recorrer con for
for elemento in lista:
    print(elemento)  

# Recorrer con índice
for i, elemento in enumerate(lista):
    print(f"Índice {i}: {elemento}")
```

### 6. Operaciones útiles

```python
len(lista)  # Cantidad de elementos  
sum(lista)  # Suma de elementos (si son números)  
max(lista)  # Valor máximo  
min(lista)  # Valor mínimo  
sorted(lista)  # Ordena sin modificar  
lista.sort()  # Ordena en la lista original  
lista.reverse()  # Invierte la lista  
```

### 7. Verificar elementos

```python
if 10 in lista:
    print("10 está en la lista")
```

### 8. Copiar una lista (evitar aliasing)

```python
copia1 = lista[:]  # Copia mediante slicing
copia2 = lista.copy()  # Copia con método copy
import copy
copia3 = copy.deepcopy(lista)  # Copia profunda
```

### 9. List Comprehension (creación rápida de listas)

```python
# Lista de cuadrados
cuadrados = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]

# Lista de números pares
pares = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]
```

### 10. Unir y separar listas

```python
# Concatenación de listas
lista1 = [1, 2, 3]
lista2 = [4, 5, 6]
lista_completa = lista1 + lista2  # [1, 2, 3, 4, 5, 6]

# Convertir string a lista y viceversa
cadena = "Hola mundo"
lista_palabras = cadena.split()  # ['Hola', 'mundo']
nueva_cadena = " ".join(lista_palabras)  # "Hola mundo"
```

### 11. Eliminar duplicados en una lista

```python
lista_duplicados = [1, 2, 2, 3, 4, 4, 5]
lista_sin_duplicados = list(set(lista_duplicados))  # [1, 2, 3, 4, 5]
```

### 12. Extender listas

```python
lista1.extend(lista2)  # Agrega los elementos de lista2 a lista1
```

### 13. Desempaquetado de listas

```python
lista = [1, 2, 3]
a, b, c = lista  # a=1, b=2, c=3
```

### 14. Iterar en paralelo con zip

```python
nombres = ["Ana", "Luis", "Carlos"]
edades = [25, 30, 22]
for nombre, edad in zip(nombres, edades):
    print(f"{nombre} tiene {edad} años")
```

### 15. Filtrar listas

```python
numeros = [1, 2, 3, 4, 5, 6]
pares = list(filter(lambda x: x % 2 == 0, numeros))  # [2, 4, 6]
```

---

Con esto ya tienes toda la información esencial sobre listas en Python. ¿Seguimos con diccionarios?