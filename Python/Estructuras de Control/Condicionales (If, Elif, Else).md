
## Estructura básica
```python
if condicion:
    # Código si la condición es verdadera
elif otra_condicion:
    # Código si la otra condición es verdadera
else:
    # Código si ninguna condición se cumple
```

## Operadores de comparación
- `==` Igualdad
- `!=` Diferente
- `>` Mayor que
- `<` Menor que
- `>=` Mayor o igual
- `<=` Menor o igual

## Operadores lógicos
- `and` (Y lógico) → Ambas condiciones deben ser verdaderas.
- `or` (O lógico) → Al menos una condición debe ser verdadera.
- `not` (Negación) → Invierte el valor lógico.

```python
x = 10
y = 20
if x < y and y > 15:
    print("Ambas condiciones son verdaderas")
```

## Condicionales anidados
```python
x = 10
if x > 5:
    if x < 20:
        print("x está entre 5 y 20")
```

## Expresión condicional (Operador ternario)
```python
mensaje = "Es mayor" if x > 18 else "Es menor"
print(mensaje)
```

## Uso con `in`
```python
vocales = "aeiou"
letra = "a"
if letra in vocales:
    print("Es una vocal")
```

## Uso con `is`
```python
x = None
if x is None:
    print("x es None")
```

## Ejemplo práctico
```python
edad = int(input("Ingrese su edad: "))
if edad >= 18:
    print("Eres mayor de edad")
else:
    print("Eres menor de edad")
