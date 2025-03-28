
### **1. G1GC (Garbage-First Garbage Collector)**

- **Características**:
    
    - Fue diseñado para aplicaciones con requisitos de baja latencia y grandes heaps.
        
    - Divide el heap en regiones de tamaño fijo, lo que permite gestionar la memoria de manera más eficiente.
        
    - **Objetivo:** Reducir los tiempos de pausa de la recolección de basura mientras mantiene una alta eficiencia.
        
- **Ventajas**:
    
    - Buena para aplicaciones que requieren un tiempo de pausa predecible y controlado.
        
    - Ideal para sistemas con heaps grandes (en servidores).
        
- **Desventajas**:
    
    - Menor rendimiento que otros GC en escenarios sin requisitos estrictos de latencia.
        
- **Configuración**:
    
    - `-XX:+UseG1GC`
        

### **2. ZGC (Z Garbage Collector)**

- **Características**:
    
    - **Enfoque:** GC de baja latencia, diseñado para evitar pausas largas.
        
    - Utiliza técnicas como la compresión de punteros y la gestión de memoria concurrente.
        
    - **Objetivo:** Latencia constante (menos de 10ms) incluso en heaps grandes (de terabytes).
        
    - Utiliza múltiples hilos para la recolección de basura, garantizando tiempos de pausa predecibles.
        
- **Ventajas**:
    
    - Muy adecuado para aplicaciones de baja latencia, con heaps grandes y memoria en sistemas de alta concurrencia.
        
- **Desventajas**:
    
    - Requiere JDK 11 o superior.
        
    - No está tan optimizado como otros GC en cuanto a la velocidad pura.
        
- **Configuración**:
    
    - `-XX:+UseZGC`
        

### **3. Shenandoah GC**

- **Características**:
    
    - Similar a ZGC, diseñado para minimizar las pausas.
        
    - **Enfoque:** Recolección concurrente y paralela, con enfoque en la reducción de pausas.
        
    - Ejecuta la mayoría de las actividades del GC de manera concurrente con la aplicación, limitando las pausas a tiempos muy cortos.
        
- **Ventajas**:
    
    - Muy bajo tiempo de pausa (menos de 10ms) en aplicaciones que requieren baja latencia.
        
    - Beneficioso para sistemas con mucha concurrencia y de gran tamaño.
        
- **Desventajas**:
    
    - Más reciente que otros recolectores, lo que puede implicar una menor estabilidad en algunos casos.
        
- **Configuración**:
    
    - `-XX:+UseShenandoahGC`
        

### **4. Parallel GC (Throughput Collector)**

- **Características**:
    
    - Se centra en maximizar el rendimiento general a costa de pausas más largas.
        
    - Utiliza múltiples hilos para la recolección de basura.
        
    - **Enfoque:** Optimiza la cantidad de trabajo realizado en cada ciclo de GC, buscando la máxima eficiencia.
        
- **Ventajas**:
    
    - Buen rendimiento general para aplicaciones donde las pausas más largas no son un problema.
        
    - Ideal para sistemas donde la eficiencia es más importante que la latencia.
        
- **Desventajas**:
    
    - Las pausas pueden ser más largas en comparación con G1GC, ZGC o Shenandoah.
        
- **Configuración**:
    
    - `-XX:+UseParallelGC`
        

### **Comparación Rápida**

|**GC**|**Objetivo**|**Ventajas**|**Desventajas**|**Configuración**|
|---|---|---|---|---|
|**G1GC**|Baja latencia y control de pausas.|Control de pausas y eficiencia en heaps grandes.|Menor rendimiento que otros GC en cargas altas.|`-XX:+UseG1GC`|
|**ZGC**|Latencia mínima, heaps grandes.|Pausas muy cortas (< 10ms), escalabilidad.|Requiere JDK 11+ y no es tan rápido en rendimiento.|`-XX:+UseZGC`|
|**Shenandoah GC**|Latencia mínima, enfoque en concurrencia.|Muy bajas pausas, ideal para baja latencia.|Nuevos en comparación con otros, menos optimizados.|`-XX:+UseShenandoahGC`|
|**Parallel GC**|Máximo rendimiento (a costa de pausas largas).|Buen rendimiento general, escalabilidad.|Pausas largas, no adecuado para sistemas sensibles a latencia.|`-XX:+UseParallelGC`|

### **Resumen**

- **G1GC:** Ideal para aplicaciones con grandes heaps y requisitos de baja latencia.
    
- **ZGC y Shenandoah:** Optimizados para latencia mínima, adecuados para sistemas con heaps grandes.
    
- **ParallelGC:** Mejor rendimiento general, pero con pausas más largas, adecuado cuando la latencia no es una preocupación.