
### Uso de `threading.Thread` y `multiprocessing.Process`

Python ofrece dos módulos principales para manejar concurrencia y paralelismo:

1. **`threading.Thread`** → Para **ejecutar múltiples hilos** dentro de un mismo proceso.
2. **`multiprocessing.Process`** → Para **crear múltiples procesos** en diferentes núcleos de CPU.

---

## 🧵 `threading.Thread` (Manejo de Hilos)

**📌 Características:**
- Ejecuta múltiples tareas concurrentemente dentro del **mismo proceso**.
- Adecuado para tareas **I/O-bound** (red, archivos, bases de datos).
- **No** aprovecha múltiples núcleos de CPU debido al **GIL (Global Interpreter Lock)**.

### 🔹 Ejemplo de `threading.Thread`

```python
import threading
import time

def tarea(nombre):
    print(f"Iniciando hilo {nombre}")
    time.sleep(2)
    print(f"Finalizando hilo {nombre}")

# Crear hilos
hilo1 = threading.Thread(target=tarea, args=("Hilo 1",))
hilo2 = threading.Thread(target=tarea, args=("Hilo 2",))

# Iniciar hilos
hilo1.start()
hilo2.start()

# Esperar a que terminen
hilo1.join()
hilo2.join()

print("Todos los hilos han finalizado")
```

📌 **Explicación:**
- Se crean **dos hilos** (`hilo1` y `hilo2`).
- `start()` inicia la ejecución en paralelo.
- `join()` espera a que terminen antes de continuar.

**✅ Cuándo usar `threading.Thread`**
- Descargar datos desde múltiples APIs al mismo tiempo.
- Leer o escribir archivos en paralelo.
- Ejecutar múltiples consultas a bases de datos.

---

## 🏭 `multiprocessing.Process` (Manejo de Procesos)

**📌 Características:**
- Crea múltiples procesos **independientes**, cada uno con su propia memoria.
- Ideal para tareas **CPU-bound** (cálculos intensivos, ML, procesamiento de datos).
- **No** está limitado por el **GIL**, lo que permite paralelismo real.

### 🔹 Ejemplo de `multiprocessing.Process`

```python
import multiprocessing
import time

def tarea(nombre):
    print(f"Iniciando proceso {nombre}")
    time.sleep(2)
    print(f"Finalizando proceso {nombre}")

if __name__ == "__main__":
    proceso1 = multiprocessing.Process(target=tarea, args=("Proceso 1",))
    proceso2 = multiprocessing.Process(target=tarea, args=("Proceso 2",))

    proceso1.start()
    proceso2.start()

    proceso1.join()
    proceso2.join()

    print("Todos los procesos han finalizado")
```

📌 **Explicación:**
- Se crean **dos procesos independientes**.
- Cada proceso tiene su propia memoria y se ejecuta en un núcleo de CPU distinto.
- `start()` inicia el proceso y `join()` espera a que termine.

**✅ Cuándo usar `multiprocessing.Process`**
- Procesamiento de grandes volúmenes de datos en Pandas o NumPy.
- Aplicaciones de Machine Learning que usan varios núcleos de CPU.
- Cálculos matemáticos intensivos.

---

## 🏆 Comparación Rápida: `threading.Thread` vs `multiprocessing.Process`

| Característica        | `threading.Thread` 🧵    | `multiprocessing.Process` 🏭 |
|----------------------|----------------------|---------------------------|
| Uso principal       | Tareas **I/O-bound**  | Tareas **CPU-bound**      |
| Afectado por el GIL | ✅ Sí                 | ❌ No                     |
| Compartición de memoria | ✅ Sí (mismo proceso) | ❌ No (memoria separada)   |
| Creación rápida     | ✅ Sí                 | ❌ No (overhead alto)      |
| Uso de múltiples núcleos | ❌ No               | ✅ Sí                     |

---

## 🔥 ¿Cuándo usar cada uno?

✅ Usa **`threading.Thread`** si tu programa depende de operaciones **I/O-bound** (red, archivos, bases de datos).  
✅ Usa **`multiprocessing.Process`** si necesitas realizar **cálculos intensivos** y aprovechar múltiples núcleos.  

Ejemplo en **Data Engineering**:
- **Threading:** Descarga de múltiples archivos desde la web en paralelo.  
- **Multiprocessing:** Procesamiento de datos en grandes volúmenes con Pandas.  
