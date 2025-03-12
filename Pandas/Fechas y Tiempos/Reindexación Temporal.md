
# Reindexado Temporal en Pandas: `resample()`, `shift()`, `rolling()`

El reindexado temporal es un concepto clave cuando trabajamos con series temporales en **Pandas**. Nos permite realizar operaciones como cambiar la frecuencia de los datos, desplazar los valores a lo largo del tiempo o aplicar ventanas móviles para suavizar o agregar datos. Las funciones **`resample()`**, **`shift()`** y **`rolling()`** son herramientas poderosas para realizar estas tareas de manera eficiente.

## **1. `resample()`**: Cambio de Frecuencia Temporal

La función **`resample()`** permite cambiar la frecuencia de los datos temporales. Esto es útil cuando tienes datos con una frecuencia irregular y necesitas convertirlos a una frecuencia uniforme (por ejemplo, de diaria a mensual).

### Ejemplo: Resampling de datos diarios a mensuales

```python
import pandas as pd

# Crear una serie temporal diaria
dates = pd.date_range('2021-01-01', periods=5, freq='D')
data = [100, 200, 300, 400, 500]
df = pd.DataFrame(data, index=dates, columns=['value'])

# Resample a mensual y aplicar agregación
df_resampled = df.resample('M').sum()  # Sumar los valores por mes
print(df_resampled)
```

En este caso, hemos cambiado la frecuencia de los datos de diaria a mensual utilizando **`'M'`** para indicar el muestreo mensual. La función **`sum()`** se usa para agregar los valores dentro de cada mes.

### Argumentos comunes para `resample()`:
- `'D'`: Diario
- `'W'`: Semanal
- `'M'`: Mensual
- `'A'`: Anual
- `'H'`: Horario

## **2. `shift()`**: Desplazamiento de Datos Temporales

La función **`shift()`** permite desplazar los valores de una serie temporal hacia adelante o hacia atrás en el tiempo. Esto es útil para calcular cambios, diferencias o para crear características basadas en valores pasados.

### Ejemplo: Desplazar datos hacia atrás y hacia adelante

```python
# Desplazar valores hacia adelante y hacia atrás
df_shifted_forward = df.shift(1)  # Desplazar 1 día hacia adelante
df_shifted_backward = df.shift(-1)  # Desplazar 1 día hacia atrás

print(df_shifted_forward)
print(df_shifted_backward)
```

**`shift()`** permite especificar el número de períodos a desplazar, con valores positivos para desplazar hacia adelante y negativos para desplazar hacia atrás. Es común usar esta función para calcular diferencias entre valores consecutivos, como en el caso de cambios diarios.

### Ejemplo de uso con diferencias:

```python
# Calcular la diferencia diaria
df['diff'] = df['value'] - df['value'].shift(1)
print(df)
```

## **3. `rolling()`**: Ventanas Móviles

La función **`rolling()`** permite aplicar una operación en una ventana móvil de los datos. Es ideal para suavizar series temporales, calcular medias móviles, sumas acumuladas, entre otros.

### Ejemplo: Media Móvil

```python
# Calcular la media móvil con una ventana de 2 períodos
df['rolling_mean'] = df['value'].rolling(window=2).mean()
print(df)
```

En este caso, estamos calculando la media móvil de los valores utilizando una ventana de 2 períodos. Puedes ajustar el tamaño de la ventana según sea necesario.

### Operaciones comunes con `rolling()`:
- **`mean()`**: Media móvil.
- **`sum()`**: Suma acumulada en la ventana.
- **`min()`** / **`max()`**: Mínimo o máximo en la ventana.
- **`std()`**: Desviación estándar en la ventana.

### Ejemplo: Suma Móvil

```python
# Calcular la suma móvil con una ventana de 3 períodos
df['rolling_sum'] = df['value'].rolling(window=3).sum()
print(df)
```

## **Conclusión**:

- **`resample()`** es ideal para cambiar la frecuencia de los datos temporales.
- **`shift()`** es útil para desplazar los datos hacia adelante o hacia atrás, permitiendo calcular diferencias entre períodos.
- **`rolling()`** es perfecto para aplicar funciones en una ventana móvil, como medias y sumas móviles.

Estas funciones son esenciales cuando trabajamos con datos temporales y queremos hacer análisis como suavizados, agregaciones o generar nuevas características basadas en el tiempo.
