
El módulo `re` permite buscar patrones en textos usando expresiones regulares.

---

## 🔹 Métodos Básicos de `re`

```python
import re
```

### 1️⃣ `search()`: Busca la primera coincidencia  
```python
texto = "Mi email es ejemplo@email.com"
patron = r"\w+@\w+\.\w+"

coincidencia = re.search(patron, texto)
if coincidencia:
    print(coincidencia.group())  # "ejemplo@email.com"
```

📌 **Nota:** Retorna un objeto `Match` o `None` si no encuentra nada.

---

### 2️⃣ `match()`: Verifica si el inicio del texto coincide  
```python
patron = r"Hola"
print(re.match(patron, "Hola mundo"))  # Match encontrado
print(re.match(patron, "Adiós mundo"))  # None
```

---

### 3️⃣ `findall()`: Encuentra todas las coincidencias  
```python
texto = "Correos: uno@email.com, dos@mail.com"
patron = r"\w+@\w+\.\w+"

correos = re.findall(patron, texto)
print(correos)  # ['uno@email.com', 'dos@mail.com']
```

---

### 4️⃣ `sub()`: Reemplazar texto con regex  
```python
texto = "Mi número es 123-456-789"
nuevo_texto = re.sub(r"\d", "X", texto)  # Reemplaza todos los dígitos
print(nuevo_texto)  # "Mi número es XXX-XXX-XXX"
```

---

## 🔹 Caracteres Especiales en Regex

| Símbolo | Significado | Ejemplo | Coincidencia |
|---------|------------|---------|-------------|
| `.` | Cualquier carácter | `c.t` | "cat", "cut" |
| `\d` | Dígito (0-9) | `\d+` | "123", "42" |
| `\w` | Letra, número o guion bajo | `\w+` | "abc_123" |
| `\s` | Espacio, tab o salto de línea | `\s+` | " " |
| `^` | Inicio de línea | `^Hola` | "Hola mundo" |
| `$` | Fin de línea | `mundo$` | "Hola mundo" |
| `*` | 0 o más repeticiones | `a*` | "", "a", "aaa" |
| `+` | 1 o más repeticiones | `a+` | "a", "aaa" |
| `?` | 0 o 1 repetición | `colou?r` | "color", "colour" |
| `{n,m}` | Entre `n` y `m` repeticiones | `\d{2,4}` | "23", "2024" |
| `[]` | Uno de los caracteres dentro | `[aeiou]` | "a", "e" |
| `()` | Agrupación | `(abc)+` | "abc", "abcabc" |

---

## 🔥 Resumen

| Método | Descripción |
|--------|------------|
| `search(patron, texto)` | Busca la primera coincidencia |
| `match(patron, texto)` | Verifica si el texto empieza con el patrón |
| `findall(patron, texto)` | Encuentra todas las coincidencias |
| `sub(patron, reemplazo, texto)` | Reemplaza coincidencias |
