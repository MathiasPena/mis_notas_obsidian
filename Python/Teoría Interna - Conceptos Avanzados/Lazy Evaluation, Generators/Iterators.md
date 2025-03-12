# Python para Data Engineering - Teoría Interna y Conceptos Avanzados

## 20. Iteradores y el Protocolo de Iteración (`__iter__`, `__next__`)

En Python, los **iteradores** son objetos que permiten recorrer elementos de manera secuencial.  
El protocolo de iteración define cómo un objeto puede ser iterado con los métodos `__iter__()` y `__next__()`.

---

## 🔹 ¿Qué es un Iterador?

Un **iterador** es cualquier objeto en Python que implementa los métodos **`__iter__()`** y **`__next__()`**, permitiendo que puedas recorrer sus elementos uno a uno.

### 🛠️ Protocolo de Iteración

1. **`__iter__()`**: Este método devuelve el propio iterador. Permite que el objeto sea **iterable**.  
2. **`__next__()`**: Este método devuelve el siguiente valor de la secuencia y **lanza una excepción `StopIteration`** cuando no hay más elementos.

---

## 🔹 Crear un Iterador Personalizado

```python
class Contador:
    def __init__(self, inicio, fin):
        self.valor = inicio
        self.fin = fin

    def __iter__(self):
        return self  # Devuelve el iterador en sí mismo

    def __next__(self):
        if self.valor >= self.fin:
            raise StopIteration  # Termina la iteración
        self.valor += 1
        return self.valor - 1

# Uso del iterador personalizado
contador = Contador(1, 5)
for numero in contador:
    print(numero)  # 1, 2, 3, 4
```

📌 **Explicación:**
- `__iter__` devuelve el propio objeto, permitiendo que sea usado en un `for`.
- `__next__` devuelve el siguiente valor de la secuencia y lanza `StopIteration` cuando se alcanza el final.

---

## 🔹 Iterando con `for` y `next()`

El **bucle `for`** usa implícitamente los métodos `__iter__()` y `__next__()` de los iteradores.

### 🛠️ Ejemplo: Usando `next()` explícitamente

```python
iterador = iter([10, 20, 30])

print(next(iterador))  # 10
print(next(iterador))  # 20
print(next(iterador))  # 30
print(next(iterador))  # Lanza StopIteration
```

📌 **Explicación:**
- `iter()` convierte una secuencia en un iterador.
- `next()` devuelve el siguiente elemento o lanza `StopIteration` si ya no hay más elementos.

---

## 🔹 Diferencia entre Iterables e Iteradores

- **Iterable**: Un objeto que implementa el método `__iter__()`. Ejemplo: listas, tuplas, diccionarios.
- **Iterador**: Un objeto que implementa ambos métodos `__iter__()` y `__next__()`. Ejemplo: cualquier objeto que use `yield`.

### 🛠️ Ejemplo de iterable

```python
# Una lista es un iterable
mi_lista = [1, 2, 3]
for numero in mi_lista:
    print(numero)  # 1, 2, 3
```

📌 **Explicación:**  
Un iterable como la lista `mi_lista` tiene un método `__iter__()` implícito, lo que permite recorrer sus elementos en un bucle `for`.

---

## 🔹 Iteradores en Python: ¿Cuándo usar?

1. **Optimización de memoria**: Los iteradores permiten generar elementos bajo demanda, sin necesidad de cargar grandes conjuntos de datos en memoria.
2. **Eficiencia en procesamiento de datos grandes**: Puedes procesar grandes volúmenes de datos de forma secuencial con bajo costo de memoria.
3. **Flujos de datos continuos**: Ideales para procesamiento en **streams**, como leer grandes archivos o datos en tiempo real.

---

## 🚀 Conclusión

- **Iteradores** son objetos que permiten recorrer datos de manera secuencial.
- El **protocolo de iteración** usa los métodos `__iter__()` y `__next__()` para que un objeto sea iterado en un bucle `for` o con `next()`.
- Los **generadores** implementan este protocolo y permiten crear secuencias de manera eficiente, generando los valores bajo demanda.

📌 **Usar iteradores es ideal cuando se necesita recorrer grandes volúmenes de datos sin cargar todo en memoria**.
