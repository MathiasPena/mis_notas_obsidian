# Python para Data Engineering - Teoría Interna y Conceptos Avanzados

## 18. Task Queues con `queue.Queue` y `asyncio.Queue`

Las **Task Queues** son estructuras que permiten gestionar tareas de forma **ordenada y concurrente**.  
Python ofrece dos tipos principales:

- `queue.Queue` → Para **threading** (tareas en paralelo con múltiples hilos).
- `asyncio.Queue` → Para **asyncio** (ejecución asíncrona sin bloqueo).

---

## 🔹 `queue.Queue` para multi-threading

`queue.Queue` se usa con **hilos (`threading.Thread`)** para manejar tareas concurrentes.

### 🛠️ Ejemplo: Productor-Consumidor con `queue.Queue`

```python
import queue
import threading
import time

def productor(q):
    for i in range(5):
        print(f"Produciendo tarea {i}")
        q.put(i)  # Agrega una tarea a la cola
        time.sleep(1)

def consumidor(q):
    while not q.empty():
        tarea = q.get()  # Obtiene una tarea de la cola
        print(f"Procesando tarea {tarea}")
        time.sleep(2)
        q.task_done()  # Marca la tarea como completada

q = queue.Queue()

# Crear hilos para el productor y consumidor
t1 = threading.Thread(target=productor, args=(q,))
t2 = threading.Thread(target=consumidor, args=(q,))

t1.start()
t2.start()

t1.join()
t2.join()
print("Todas las tareas fueron procesadas")
```

📌 **Explicación:**  
- `q.put(i)` agrega elementos a la cola.  
- `q.get()` extrae tareas de la cola.  
- `q.task_done()` marca la tarea como finalizada.  
- `threading.Thread` permite ejecutar productor y consumidor en paralelo.  

✅ **Ideal para tareas multi-threading como procesamiento de logs o scraping**.

---

## 🔹 `asyncio.Queue` para ejecución asíncrona

`asyncio.Queue` es una **cola asíncrona** diseñada para `asyncio`, evitando bloqueos.

### 🛠️ Ejemplo: Productor-Consumidor con `asyncio.Queue`

```python
import asyncio

async def productor(q):
    for i in range(5):
        print(f"Produciendo tarea {i}")
        await q.put(i)  # Agrega tarea a la cola
        await asyncio.sleep(1)

async def consumidor(q):
    while True:
        tarea = await q.get()  # Obtiene tarea
        print(f"Procesando tarea {tarea}")
        await asyncio.sleep(2)
        q.task_done()  # Marca como finalizada

async def main():
    q = asyncio.Queue()

    # Lanza productor y consumidor
    productor_task = asyncio.create_task(productor(q))
    consumidor_task = asyncio.create_task(consumidor(q))

    await productor_task  # Espera que el productor termine
    await q.join()  # Espera que la cola se vacíe
    consumidor_task.cancel()  # Detiene el consumidor

asyncio.run(main())
```

📌 **Explicación:**  
- `await q.put(i)` agrega tareas de forma **asíncrona**.  
- `await q.get()` extrae tareas **sin bloquear el event loop**.  
- `q.task_done()` indica que la tarea se completó.  
- `await q.join()` espera que todas las tareas terminen.  

✅ **Ideal para manejar flujos de trabajo en ETL o procesamiento en tiempo real**.

---

## 🚀 Comparación `queue.Queue` vs `asyncio.Queue`

| Característica        | `queue.Queue` 🧵 (Threading) | `asyncio.Queue` ⚡ (Asyncio) |
|----------------------|----------------|----------------|
| Bloquea ejecución   | ✅ Sí (Bloqueante) | ❌ No (No bloqueante) |
| Uso principal       | Hilos (`threading.Thread`) | Async (`async def`) |
| Operaciones I/O     | ❌ No optimizado | ✅ Ideal para I/O-bound |
| Complejidad         | 🔹 Media | 🔹 Media |

✅ **Cuándo usar `queue.Queue`**
- Cuando usas `threading.Thread` para **tareas CPU-bound ligeras**.  
- Para procesar trabajos en **background** dentro de una aplicación.  

✅ **Cuándo usar `asyncio.Queue`**
- Si tu aplicación usa `asyncio` y necesita **gestionar tareas sin bloquear**.  
- Para consumir datos de APIs, bases de datos o flujos de datos en **tiempo real**.  

---

🚀 **Conclusión:**  
- **Para multi-threading**, usa `queue.Queue`.  
- **Para asyncio**, usa `asyncio.Queue`.  
- Ambos permiten **gestionar tareas concurrentemente**, pero en diferentes modelos de ejecución.  
