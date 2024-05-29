

----
- TAG:
----
Los operadores aritméticos son símbolos que Python utiliza para realizar cálculos matemáticos.

Los fundamentales son:

- **Suma (+)**: No solo suma números, sino que también une secuencias como cadenas y listas, creando una nueva secuencia que es la combinación de ambas.
- **Resta (-)**: Se utiliza para restar un número de otro. Con listas, su uso es menos directo y generalmente no se aplica como operador directo.
- **Multiplicación (*)**: Cuando se multiplica un número por otro, obtenemos el producto. Con cadenas y listas, este operador repite los elementos la cantidad de veces especificada.
- **División (/)**: Divide un número entre otro y el resultado es siempre un número flotante, incluso si los números son enteros.
- **Exponente (**):** Eleva un número a la potencia de otro. Por ejemplo, ‘**2 ** 3**‘ resultará en 8. Este operador es menos común en operaciones con cadenas o listas.

**Operaciones con Cadenas**

En Python, las cadenas son objetos que representan secuencias de caracteres y se pueden manipular usando operadores aritméticos:

- **Concatenación (+)**: Une varias cadenas en una sola. Por ejemplo, ‘Hola’ + ‘ ‘ + ‘Mundo’ se convierte en ‘Hola Mundo’.
- **Repetición (*)**: Crea repeticiones de la misma cadena. ‘Hola’ * 3 generará ‘HolaHolaHola’.

**Operaciones con Listas**

Las listas son colecciones ordenadas y mutables de elementos:

- **Concatenación (+)**: Similar a las cadenas, unir dos listas las combina en una nueva lista.
- **Repetición (*)**: Repite todos los elementos de la lista un número determinado de veces.

**Funciones Especiales para Listas**

- **Zip**: Toma dos o más listas y las empareja, creando una lista de tuplas. Cada tupla contiene elementos de las listas originales que ocupan la misma posición.
- **Map**: Aplica una función específica a cada elemento de un iterable, lo que resulta útil para transformar los datos contenidos.

Asimismo, otro de los conceptos que mencionamos es el de ‘**TypeCast**‘. El TypeCast, o conversión de tipo, es el proceso mediante el cual se cambia una variable de un tipo de dato a otro.

En Python, esto se realiza de manera muy directa, utilizando el nombre del tipo de dato como una función para realizar la conversión. Por ejemplo, convertir una cadena a un entero se hace pasando la cadena como argumento a la función **int()**, y transformar un número a una cadena se hace con la función **str()**. Esta capacidad de cambiar el tipo de dato es especialmente útil cuando se necesita estandarizar los tipos de datos para operaciones específicas o para cumplir con los requisitos de las estructuras de datos.

A medida que progresemos, ampliaremos nuestro repertorio para incluir operaciones más complejas y explorar otros tipos de datos y estructuras en Python.

-----
# Operadores y Operaciones básicas en python

Vamo a crear un ejemplos básicos para que esto quede muy claro, empezamos creando un archivo que se llame `test.py` 

Empezamos creando una variable para la practica 
```python
#/usr/bin/python

first_number = 2
second_number = 8

print(first_number + second_number)
```

O podríamos realizaar la misma operatoria de la siguiente manera 
```python
#/usr/bin/python

first_number = 2
second_number = 8

result = firts_number + second_number

print(type(result))
```

 De igual manera lo podemos hacer con la resta, multiplicación y división tan solo cambiando  el signo correspondiente antes del signo `+` 

Tambien se puede elevar a la potencia con soble asterisco `**` 

Si deseamos rendondear las respuestas lo podemos hacer con la función `round` 
```python
#/usr/bin/python

first_number = 2
second_number = 8

result = firts_number + second_number

print(round(result, 2))
```

Ahora hablaremos un poco sobre los formateos en las salidas de respuesta en python, consiste en el proceso de convertir datos a una representación especifícia o estructura, es decir darles un formato especifico a estos datos siguiendo un tipo se reglas en específico

Podríamos hacer lo siguiente para poder añadir puntos o comas en los números para destinguir si son miles, cientos etc
```python
#/usr/bin/python

first_number = 2
second_number = 8

result = firts_number ** second_number

print("{:,}".format(result))
```

Aqui podríamos sustituir las comas por los puntos
```python
#/usr/bin/python

first_number = 2
second_number = 8

result = firts_number ** second_number

print(round("{:,}".format(result).replace(",", "."))
```

Aca tendriamos otro operador con el `%` para poder obtener el resto de esa división 

Ahora realizaremos operaciones con cadenas 
```python

firts_str = "Hola"
second_str = " "
third_str  = "Mundo"

print(firts_str + second_str + third_str)
```

Esto nos daria de resultado por consola un `Hola Mundo` 
La función `print(firts_str*3)` nos imprime por 3 la palabra Hola ubicada en `firts_str` 
En cambio si solo desearamos repetir una palabra en especifico puede ser con `print(firts_str[0]*8)` 
Tambien podemos jugar por rangos con `print(third_str[0:3]*5)` para imprimir en un rango de 5 veces la palabra `MunMunMun`


Tambien podemos realizar operaciones con listas y muchas cosas mas, en el siguiente ejemplo veremos como compactar la información de dos variables
```python
#!/usr/bin/python3

first_elements = [1, 3, 5, 7, 9]
second_elements = [2, 4, 6, 8]

result = first_elements + second_elements

print(result)
```

Si desean mostrar los numeros en paralelo y en orden lo pueden hacer de la siguiente manera
```python
#!/usr/bin/python3

odd_numbers = [1, 3, 5, 7, 9]
even_numbers = [2, 4, 6, 8]

result = zip(odd_numbers, even_numbers)

for element in result:
	print(element)
```


Ahora si desean sumar los numeros en paralelo pueden hacer la siguiente función 
```python
#!/usr/bin/python3

odd_numbers = [1, 3, 5, 7, 9]
even_numbers = [2, 4, 6, 8, 10]

result = map(sum, zip(odd_numbers, even_numbers))

for element in result:
	print(element)
```

Y finalmente para fucionarla en una sola lista en la salida por consola, lo podemos hacer de la siguiente manera
```python
#!/usr/bin/python3

odd_numbers = [1, 3, 5, 7, 9]
even_numbers = [2, 4, 6, 8, 10]

result = list(map(sum, zip(odd_numbers, even_numbers)))

print(result)
```
