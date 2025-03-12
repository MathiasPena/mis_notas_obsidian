 
### 🔹 Generadores (`yield`) vs Listas Normales  

En Python, los **generadores** permiten la **evaluación perezosa** (**lazy evaluation**), generando elementos **uno a uno** en lugar de cargar toda la secuencia en memoria.  
Esto los hace más eficientes en términos de **uso de memoria y rendimiento**.

---

## 🚀 ¿Qué diferencia hay entre Generadores y Listas?

| Característica         | Listas Normales (`[]`) | Generadores (`yield`) |
|-----------------------|----------------|----------------|
| Almacenamiento       | En memoria (RAM) | Genera elementos sobre la marcha |
| Tiempo de ejecución  | Rápido para listas pequeñas | Eficiente para datos grandes |
| Consumo de memoria   | Alto si la lista es grande | Mínimo (solo almacena el estado actual) |
| Iteración            | Itera sobre todos los elementos a la vez | Genera cada elemento cuando es necesario |
| Uso recomendado      | Para conjuntos de datos pequeños | Para grandes volúmenes de datos o streams |

✅ **Los generadores son ideales cuando se trabaja con grandes datasets, archivos, o streams de datos en tiempo real.**  

---

## 🔹 Ejemplo: Lista vs Generador

```python
# Lista normal: carga todos los números en memoria
numeros_lista = [x**2 for x in range(10)]
print(numeros_lista)  # [0, 1, 4, 9, 16, ..., 81]

# Generador: calcula cada número sobre la marcha
def numeros_generador():
    for x in range(10):
        yield x**2  # Devuelve un valor sin almacenar en memoria

gen = numeros_generador()
print(next(gen))  # 0
print(next(gen))  # 1
print(next(gen))  # 4
```

📌 **Diferencia clave:**  
- La **lista** almacena **todos los valores** en memoria.  
- El **generador** produce **solo un valor a la vez**.  

---

## 🔹 `yield` vs `return`  

| Característica | `return` | `yield` |
|--------------|---------|--------|
| Tipo de función | Devuelve un valor y finaliza | Devuelve un valor pero mantiene el estado |
| Persistencia | Pierde el estado tras ejecutar | Mantiene el estado entre llamadas |
| Iteración | No se puede iterar | Se puede usar con `next()` o en loops |

### 🛠️ Ejemplo de `yield`

```python
def contador():
    print("Inicio del generador")
    yield 1
    yield 2
    yield 3

gen = contador()
print(next(gen))  # "Inicio del generador" → 1
print(next(gen))  # 2
print(next(gen))  # 3
```

✅ **El generador mantiene su estado entre ejecuciones**.  

---

## 🔹 ¿Cuándo usar Generadores?  

1️⃣ **Procesamiento de grandes volúmenes de datos**  
   - Archivos grandes (`csv`, `json`, logs).  
   - Streaming de datos en tiempo real.  

2️⃣ **Eficiencia en memoria**  
   - En lugar de cargar millones de filas en una lista, se pueden **procesar línea por línea**.  

3️⃣ **Optimización en Data Engineering**  
   - En pipelines ETL, los generadores permiten **procesamiento eficiente sin bloquear la memoria**.  

---

## 🔹 Ejemplo: Leer archivo grande con Generadores  

```python
def leer_archivo(archivo):
    with open(archivo, "r") as f:
        for linea in f:
            yield linea.strip()  # Procesa línea por línea

for linea in leer_archivo("datos.txt"):
    print(linea)  # No carga todo el archivo en memoria
```

✅ **Esto evita cargar un archivo gigante en memoria**.  

---

🚀 **Conclusión:**  
- **Las listas** son útiles cuando los datos caben en memoria.  
- **Los generadores** son ideales para **grandes volúmenes de datos y streaming**.  
- `yield` permite evaluación perezosa, **optimizando memoria y rendimiento**.  
