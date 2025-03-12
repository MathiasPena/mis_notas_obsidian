
Python ofrece una amplia variedad de métodos integrados para manipular cadenas de texto. A continuación, se explican algunos de los más utilizados.

## 1.1 `split()`

El método `split()` divide una cadena en una lista de subcadenas, usando un delimitador específico (por defecto, los espacios).

### Sintaxis:
```python
cadena.split(separador, maxsplit)
```

- **separador**: El delimitador que se utiliza para dividir la cadena (opcional, por defecto es cualquier espacio).
- **maxsplit**: Número máximo de divisiones (opcional).

### Ejemplo:

```python
texto = "Python es increíble"
resultado = texto.split()  # Divide por espacios
print(resultado)  # ['Python', 'es', 'increíble']
```

### Ejemplo con delimitador:

```python
fecha = "2025-03-10"
resultado = fecha.split("-")  # Divide por el guion
print(resultado)  # ['2025', '03', '10']
```

## 1.2 `strip()`

El método `strip()` elimina los espacios (o caracteres especificados) al principio y al final de una cadena.

### Sintaxis:
```python
cadena.strip(caracteres)
```

- **caracteres**: Especifica qué caracteres deben eliminarse (opcional, por defecto son los espacios).

### Ejemplo:

```python
texto = "   Python   "
resultado = texto.strip()  # Elimina los espacios
print(resultado)  # 'Python'
```

### Ejemplo con caracteres:

```python
texto = "###Python###"
resultado = texto.strip("#")  # Elimina los # al principio y al final
print(resultado)  # 'Python'
```

## 1.3 `replace()`

El método `replace()` reemplaza todas las ocurrencias de una subcadena por otra.

### Sintaxis:
```python
cadena.replace(valor_antiguo, valor_nuevo, max_reemplazos)
```

- **valor_antiguo**: Subcadena que se desea reemplazar.
- **valor_nuevo**: Subcadena con la que se reemplazará.
- **max_reemplazos**: Número máximo de reemplazos (opcional).

### Ejemplo:

```python
texto = "Python es genial"
resultado = texto.replace("genial", "increíble")
print(resultado)  # 'Python es increíble'
```

### Ejemplo con límite de reemplazos:

```python
texto = "a, b, c, a"
resultado = texto.replace("a", "z", 1)  # Solo reemplaza la primera 'a'
print(resultado)  # 'z, b, c, a'
```

## 1.4 `find()`

El método `find()` busca la primera ocurrencia de una subcadena dentro de una cadena. Si la subcadena no se encuentra, devuelve `-1`.

### Sintaxis:
```python
cadena.find(subcadena, inicio, fin)
```

- **subcadena**: La cadena que estamos buscando.
- **inicio** y **fin**: Posiciones donde comienza y termina la búsqueda (opcional).

### Ejemplo:

```python
texto = "Python es increíble"
resultado = texto.find("es")
print(resultado)  # 7 (posición de la primera aparición de 'es')
```

### Ejemplo sin encontrar la subcadena:

```python
texto = "Python es increíble"
resultado = texto.find("Java")
print(resultado)  # -1 (no se encuentra 'Java')
```

## 1.5 `startswith()` y `endswith()`

Los métodos `startswith()` y `endswith()` verifican si una cadena comienza o termina con una subcadena específica.

### Sintaxis:
```python
cadena.startswith(subcadena, inicio, fin)
cadena.endswith(subcadena, inicio, fin)
```

- **subcadena**: La subcadena que se verifica.
- **inicio** y **fin**: Pueden especificar las posiciones de inicio y fin (opcional).

### Ejemplo `startswith()`:

```python
texto = "Python es genial"
resultado = texto.startswith("Python")
print(resultado)  # True
```

### Ejemplo `endswith()`:

```python
texto = "Python es genial"
resultado = texto.endswith("genial")
print(resultado)  # True
```

## 1.6 Otros Métodos Útiles

- **`lower()`**: Convierte todos los caracteres de la cadena a minúsculas.
  
  ```python
  texto = "Python"
  resultado = texto.lower()
  print(resultado)  # 'python'
  ```

- **`upper()`**: Convierte todos los caracteres de la cadena a mayúsculas.
  
  ```python
  texto = "Python"
  resultado = texto.upper()
  print(resultado)  # 'PYTHON'
  ```

- **`title()`**: Capitaliza la primera letra de cada palabra.
  
  ```python
  texto = "python es increible"
  resultado = texto.title()
  print(resultado)  # 'Python Es Increible'
  ```

- **`isalpha()`**: Verifica si la cadena contiene solo letras.
  
  ```python
  texto = "Python"
  resultado = texto.isalpha()
  print(resultado)  # True
  ```

- **`isdigit()`**: Verifica si la cadena contiene solo dígitos.
  
  ```python
  texto = "12345"
  resultado = texto.isdigit()
  print(resultado)  # True
  ```

## Resumen

- **`split()`**: Divide una cadena en una lista de subcadenas.
- **`strip()`**: Elimina caracteres (espacios por defecto) al principio y al final de la cadena.
- **`replace()`**: Reemplaza una subcadena por otra.
- **`find()`**: Busca la posición de la primera ocurrencia de una subcadena.
- **`startswith()` y `endswith()`**: Verifican si una cadena comienza o termina con una subcadena.

