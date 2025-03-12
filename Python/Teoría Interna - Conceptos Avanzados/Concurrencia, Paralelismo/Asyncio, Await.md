# Python para Data Engineering - Teoría Interna y Conceptos Avanzados

## 17. Concurrencia y Paralelismo

### Asincronía con `asyncio` y `await`

Python ofrece el módulo **`asyncio`** para manejar tareas asíncronas de manera eficiente usando **corutinas**.  
Esto permite **no bloquear** el programa mientras se esperan operaciones I/O (red, bases de datos, archivos).

---

## 🏆 ¿Por qué usar `asyncio`?
✅ Maneja múltiples tareas en paralelo sin usar hilos o procesos.  
✅ Perfecto para operaciones **I/O-bound** como consultas a APIs o bases de datos.  
✅ Más eficiente que `threading` cuando hay muchas operaciones de espera.  

---

## 🔹 Sintaxis básica con `async` y `await`

```python
import asyncio

async def tarea(nombre):
    print(f"Iniciando {nombre}")
    await asyncio.sleep(2)  # Simula una espera sin bloquear
    print(f"Finalizando {nombre}")

async def main():
    await asyncio.gather(tarea("Tarea 1"), tarea("Tarea 2"))

asyncio.run(main())  # Ejecuta el event loop
```

📌 **Explicación:**  
- `async def` define una **corutina** (función asíncrona).  
- `await asyncio.sleep(2)` simula una espera **sin bloquear** el programa.  
- `asyncio.gather(tarea1, tarea2)` ejecuta ambas tareas en **paralelo**.  
- `asyncio.run(main())` inicia el **event loop**.  

---

## 🔥 Ejemplo: Descarga asíncrona de datos con `aiohttp`

```python
import asyncio
import aiohttp

async def descargar(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            print(f"Descargando {url} - Status {response.status}")
            return await response.text()

async def main():
    urls = [
        "https://jsonplaceholder.typicode.com/posts/1",
        "https://jsonplaceholder.typicode.com/posts/2",
    ]
    respuestas = await asyncio.gather(*[descargar(url) for url in urls])
    print("Descargas completadas")

asyncio.run(main())
```

📌 **Explicación:**  
- `aiohttp.ClientSession()` permite hacer **peticiones HTTP asíncronas**.  
- `async with session.get(url)` envía la solicitud **sin bloquear**.  
- `await response.text()` obtiene el contenido cuando esté listo.  
- **Todas las descargas se ejecutan en paralelo** gracias a `asyncio.gather()`.  

---

## 🚀 `asyncio` en Data Engineering  

✅ **Conexiones asíncronas a bases de datos** (Ej: `asyncpg` para PostgreSQL).  
✅ **Procesamiento de logs en tiempo real** sin bloquear el flujo principal.  
✅ **Paralelizar consultas a múltiples APIs** para ETL de datos.  

---

## 🏆 Diferencias: `asyncio` vs `threading`

| Característica        | `asyncio` 🕒 | `threading.Thread` 🧵 |
|----------------------|-------------|----------------------|
| Bloquea la ejecución | ❌ No        | ✅ Sí (GIL afecta)  |
| Uso de hilos         | ❌ No        | ✅ Sí               |
| Mejor para          | **I/O-bound** (APIs, DBs) | **I/O-bound** (archivos, red) |
| Complejidad         | 🔹 Media     | 🔹 Baja             |

---

✅ **Cuándo usar `asyncio` en vez de `threading`**
- **Si tienes muchas tareas I/O-bound** (consultas a APIs, bases de datos).  
- **Si quieres evitar hilos y compartir menos memoria**.  
- **Si necesitas eficiencia y escalabilidad en operaciones asíncronas**.  

🚀 **Combinar `asyncio` con `multiprocessing` puede maximizar el rendimiento**. 🔥  
