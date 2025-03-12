
### Strategy Pattern con funciones de orden superior

El **Strategy Pattern** es un patrón de diseño de comportamiento que permite definir un conjunto de algoritmos, encapsularlos y hacerlos intercambiables sin modificar el código cliente. En Python, se puede implementar de manera sencilla utilizando **funciones de orden superior** y **first-class functions**, sin necesidad de clases adicionales.

---

## Implementación con funciones de orden superior

En lugar de definir clases para cada estrategia, podemos aprovechar las **funciones de orden superior** para hacer que una función reciba otra como argumento y ejecute la estrategia deseada.

### 1. Definir las estrategias como funciones

```python
def estrategia_suma(a, b):
    return a + b

def estrategia_multiplicacion(a, b):
    return a * b

def estrategia_resta(a, b):
    return a - b
```

Aquí, cada estrategia es simplemente una función independiente.

---

### 2. Implementar una función que use una estrategia

```python
def ejecutar_estrategia(estrategia, a, b):
    return estrategia(a, b)
```

Esta función de orden superior recibe una estrategia como parámetro y la ejecuta con los valores dados.

---

### 3. Uso del Strategy Pattern

```python
resultado1 = ejecutar_estrategia(estrategia_suma, 5, 3)
resultado2 = ejecutar_estrategia(estrategia_multiplicacion, 5, 3)
resultado3 = ejecutar_estrategia(estrategia_resta, 5, 3)

print(resultado1)  # Output: 8
print(resultado2)  # Output: 15
print(resultado3)  # Output: 2
```

Aquí se selecciona dinámicamente la estrategia a utilizar sin modificar el código base.

---

## Implementación con diccionario de estrategias

Otra forma eficiente de implementar el patrón Strategy es usar un **diccionario de funciones**, evitando múltiples `if-elif`.

```python
estrategias = {
    "suma": estrategia_suma,
    "multiplicacion": estrategia_multiplicacion,
    "resta": estrategia_resta
}

def ejecutar_con_diccionario(nombre_estrategia, a, b):
    estrategia = estrategias.get(nombre_estrategia)
    if estrategia:
        return estrategia(a, b)
    else:
        raise ValueError("Estrategia no válida")

print(ejecutar_con_diccionario("suma", 10, 5))          # Output: 15
print(ejecutar_con_diccionario("multiplicacion", 10, 5)) # Output: 50
print(ejecutar_con_diccionario("resta", 10, 5))          # Output: 5
```

---

## Ventajas del Strategy Pattern con funciones de orden superior

✅ **Código más limpio y flexible**: No se necesita definir clases ni métodos adicionales.  
✅ **Extensible**: Se pueden agregar nuevas estrategias sin modificar el código existente.  
✅ **Más Pythonic**: Aprovecha funciones de primer orden y diccionarios para manejar estrategias de forma eficiente.  

---

## Casos de Uso Comunes

- **Algoritmos intercambiables**: Por ejemplo, diferentes métodos de ordenamiento o cálculo.  
- **Lógica de precios en e-commerce**: Aplicar diferentes estrategias de descuento dinámicamente.  
- **Manejo de logs**: Definir distintos formatos o destinos (archivo, consola, base de datos).  

---

## Resumen

El **Strategy Pattern con funciones de orden superior** permite intercambiar dinámicamente algoritmos sin necesidad de clases. Usar funciones como estrategias hace que el código sea más simple, modular y mantenible, aprovechando características propias de Python como first-class functions y diccionarios de estrategias.
