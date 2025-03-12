
### 2. **LEAD()**

La función **LEAD()** permite acceder a los valores de una fila que se encuentran después de la fila actual dentro de una ventana. Es útil para comparar los valores actuales con los valores de las filas siguientes, sin necesidad de realizar una auto-join.

#### Sintaxis:

```sql
LEAD(columna, desplazamiento, valor_por_defecto) OVER (ORDER BY columna)
```

- **columna**: La columna de la que se quiere obtener el valor.
- **desplazamiento**: La cantidad de filas hacia adelante que deseas mirar (por defecto es 1).
- **valor_por_defecto**: El valor que se devuelve si no hay fila siguiente.

#### Ejemplos:

- **LEAD() básico**:

```sql
SELECT nombre, salario, LEAD(salario) OVER (ORDER BY salario DESC) AS salario_siguiente
FROM Empleados;
```
Este ejemplo obtiene el salario del siguiente empleado en el ranking de salarios. Si un empleado es el último en el ranking, la columna `salario_siguiente` tendrá un valor `NULL`.

- **LEAD() con desplazamiento**:

```sql
SELECT nombre, salario, LEAD(salario, 2) OVER (ORDER BY salario DESC) AS salario_2_filas
FROM Empleados;
```
Aquí, se obtiene el salario del empleado que está dos filas abajo en el ranking. Si no hay un valor dos filas abajo, devolverá `NULL`.

- **LEAD() con valor por defecto**:

```sql
SELECT nombre, salario, LEAD(salario, 1, 0) OVER (ORDER BY salario DESC) AS salario_siguiente
FROM Empleados;
```
En este caso, si no hay fila siguiente (como en el caso del último empleado), se asignará el valor `0` en lugar de `NULL`.

---

### 3. **LAG()**

La función **LAG()** es lo opuesto a **LEAD()**. Permite acceder a los valores de las filas anteriores a la fila actual dentro de una ventana. Es útil cuando necesitas comparar el valor actual con el valor de las filas anteriores.

#### Sintaxis:

```sql
LAG(columna, desplazamiento, valor_por_defecto) OVER (ORDER BY columna)
```

- **columna**: La columna de la que se quiere obtener el valor.
- **desplazamiento**: La cantidad de filas hacia atrás que deseas mirar (por defecto es 1).
- **valor_por_defecto**: El valor que se devuelve si no hay fila anterior.

#### Ejemplos:

- **LAG() básico**:

```sql
SELECT nombre, salario, LAG(salario) OVER (ORDER BY salario DESC) AS salario_anterior
FROM Empleados;
```
Este ejemplo obtiene el salario del empleado anterior en el ranking de salarios. Si el empleado es el primero, la columna `salario_anterior` tendrá un valor `NULL`.

- **LAG() con desplazamiento**:

```sql
SELECT nombre, salario, LAG(salario, 2) OVER (ORDER BY salario DESC) AS salario_2_filas
FROM Empleados;
```
Aquí, se obtiene el salario del empleado que está dos filas arriba en el ranking. Si no hay un valor dos filas arriba, devolverá `NULL`.

- **LAG() con valor por defecto**:

```sql
SELECT nombre, salario, LAG(salario, 1, 0) OVER (ORDER BY salario DESC) AS salario_anterior
FROM Empleados;
```
En este caso, si no hay fila anterior (como en el caso del primer empleado), se asignará el valor `0` en lugar de `NULL`.

---

### 4. **PARTITION BY**

La cláusula **PARTITION BY** se utiliza para dividir un conjunto de resultados en particiones o grupos antes de aplicar la función de ventana. Cada partición será tratada de forma independiente por las funciones de ventana.

#### Sintaxis:

```sql
función_de_ventana() OVER (PARTITION BY columna ORDER BY columna)
```

#### Ejemplos:

- **PARTITION BY básico**:

```sql
SELECT nombre, departamento_id, salario, 
       LEAD(salario) OVER (PARTITION BY departamento_id ORDER BY salario DESC) AS salario_siguiente
FROM Empleados;
```
Este ejemplo utiliza **PARTITION BY** para aplicar la función **LEAD()** dentro de cada departamento por separado, de modo que el salario siguiente se calcula dentro de cada departamento sin mezclar a los empleados de otros departamentos.

- **PARTITION BY con varias columnas**:

```sql
SELECT nombre, departamento_id, salario, 
       RANK() OVER (PARTITION BY departamento_id, puesto ORDER BY salario DESC) AS ranking_departamento_puesto
FROM Empleados;
```
Aquí, la función **RANK()** asigna un ranking de salario dentro de cada combinación de departamento y puesto. La partición se realiza primero por **departamento_id** y luego por **puesto**.

- **PARTITION BY con LEAD()**:

```sql
SELECT nombre, salario, departamento_id,
       LEAD(salario) OVER (PARTITION BY departamento_id ORDER BY salario DESC) AS salario_siguiente
FROM Empleados;
```
En este caso, **LEAD()** se utiliza para obtener el salario del siguiente empleado dentro de su departamento específico, respetando el orden de salario dentro de cada departamento.

---

### Resumen

- **LEAD()**: Accede a los valores de una fila posterior en el conjunto de resultados, útil para comparar los valores actuales con los siguientes.
- **LAG()**: Accede a los valores de una fila anterior en el conjunto de resultados, útil para comparar los valores actuales con los anteriores.
- **PARTITION BY**: Divide el conjunto de resultados en particiones o grupos antes de aplicar funciones de ventana, permitiendo cálculos independientes por grupo.

Las funciones **LEAD()**, **LAG()** y **PARTITION BY** son muy poderosas para realizar cálculos relativos entre filas, comparando valores anteriores o posteriores dentro de particiones definidas en el conjunto de resultados.
