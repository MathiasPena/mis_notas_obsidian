
### Diferencia entre Threading vs Multiprocessing

Python ofrece dos enfoques principales para manejar tareas concurrentes: **Threading** y **Multiprocessing**. La elección entre ellos depende del tipo de tarea que se quiera ejecutar.

---

## 🧵 Threading (Múltiples Hilos)

**✅ Útil para:**  
- Tareas **I/O-bound** (espera de red, archivos, bases de datos).  
- Programas que deben realizar múltiples tareas concurrentes sin necesidad de CPU intensiva.  

**🚫 No mejora:**  
- Procesos que dependen de cálculos intensivos debido al **GIL (Global Interpreter Lock)**.

**📌 Características:**  
- Usa el módulo `threading` de Python.  
- Ejecuta múltiples hilos dentro de un solo proceso.  
- Todos los hilos comparten la misma memoria.  

### 🔹 Ejemplo de Threading

```python
import threading
import time

def tarea():
    print("Inicio de tarea en hilo")
    time.sleep(2)
    print("Fin de tarea en hilo")

hilo1 = threading.Thread(target=tarea)
hilo2 = threading.Thread(target=tarea)

hilo1.start()
hilo2.start()

hilo1.join()
hilo2.join()

print("Tareas completadas")
```

🔹 Aquí **dos hilos** se ejecutan simultáneamente. Aunque no paralelizan cálculos, permiten que otras tareas continúen mientras se espera una respuesta de I/O.

---

## 🏭 Multiprocessing (Múltiples Procesos)

**✅ Útil para:**  
- Tareas **CPU-bound** (cálculos intensivos, ML, procesamiento de datos).  
- Escalar el rendimiento aprovechando múltiples núcleos de CPU.  

**📌 Características:**  
- Usa el módulo `multiprocessing`.  
- Crea procesos independientes, evitando el **GIL**.  
- Cada proceso tiene su propio espacio de memoria (no comparten variables).  

### 🔹 Ejemplo de Multiprocessing

```python
import multiprocessing
import time

def tarea():
    print("Inicio de tarea en proceso")
    time.sleep(2)
    print("Fin de tarea en proceso")

if __name__ == "__main__":
    proceso1 = multiprocessing.Process(target=tarea)
    proceso2 = multiprocessing.Process(target=tarea)

    proceso1.start()
    proceso2.start()

    proceso1.join()
    proceso2.join()

    print("Procesos completados")
```

🔹 Aquí los procesos se ejecutan **en paralelo**, distribuyéndose en diferentes núcleos.

---

## 🔥 Comparación Rápida: Threading vs Multiprocessing

| Característica      | Threading 🧵                     | Multiprocessing 🏭        |
|--------------------|--------------------------------|-------------------------|
| Uso principal     | Tareas **I/O-bound**           | Tareas **CPU-bound**    |
| Afectado por el GIL | ✅ Sí                         | ❌ No                   |
| Compartición de memoria | ✅ Sí (mismo proceso)       | ❌ No (memoria separada) |
| Creación de hilos/procesos | ✅ Rápida                 | ❌ Lenta (overhead alto) |
| Uso de CPU        | ❌ No aprovecha múltiples núcleos | ✅ Sí, usa varios núcleos |

---

## 🏆 ¿Cuándo usar cada uno?

🔹 Usa **Threading** si tu programa depende de operaciones I/O (espera de red, archivos, bases de datos).  
🔹 Usa **Multiprocessing** si necesitas realizar cálculos intensivos y aprovechar múltiples núcleos.  

✅ **Ejemplo en Data Engineering:**  
- **Threading:** Extracción de datos de múltiples APIs al mismo tiempo.  
- **Multiprocessing:** Procesamiento en paralelo de grandes datasets con Pandas o NumPy.  
