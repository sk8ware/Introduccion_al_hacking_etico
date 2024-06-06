
----
- TAG: 
----
En esta clase, dedicaremos nuestro enfoque a las tuplas, una estructura de datos fundamental en Python que comparte algunas similitudes con las listas, pero se distingue por su inmutabilidad.

Las tuplas son colecciones ordenadas de elementos que no pueden modificarse una vez creadas. Esta característica las hace ideales para asegurar que ciertos datos permanezcan constantes a lo largo del ciclo de vida de un programa.

**Características de las Tuplas**

- **Inmutabilidad**: Una vez que se crea una tupla, no puedes cambiar, añadir o eliminar elementos. Esta inmutabilidad garantiza la integridad de los datos que desea mantener constantes.
- **Indexación y Slicing**: Al igual que las listas, puedes acceder a los elementos de la tupla mediante índices y también puedes realizar operaciones de slicing para obtener subsecuencias de la tupla.
- **Heterogeneidad**: Las tuplas pueden contener elementos de diferentes tipos, incluyendo otras tuplas, lo que las hace muy versátiles.

**Operaciones con Tuplas**

Aunque no puedes modificar una tupla, hay varias operaciones que puedes realizar:

- **Empaquetado y Desempaquetado de Tuplas**: Las tuplas permiten asignar y desasignar sus elementos a múltiples variables de forma simultánea.
- **Concatenación y Repetición**: Similar a las listas, puedes combinar tuplas usando el operador ‘**+**‘ y repetir los elementos de una tupla un número determinado de veces con el operador ‘*****‘.
- **Métodos de Búsqueda**: Puedes usar métodos como ‘**index()**‘ para encontrar la posición de un elemento y ‘**count()**‘ para contar cuántas veces aparece un elemento en la tupla.

**Uso de Tuplas en Python**

- **Funciones y Asignaciones Múltiples**: Las tuplas son muy útiles cuando una función necesita devolver múltiples valores o cuando se realizan asignaciones múltiples en una sola línea.
- **Estructuras de Datos Fijas**: Se usan para crear estructuras de datos que no deben cambiar, como los días de la semana o las coordenadas de un punto en el espacio.

**Buenas Prácticas**

Abordaremos cuándo es más apropiado utilizar tuplas en lugar de listas y cómo la elección de una tupla sobre una lista puede afectar la claridad y la seguridad del código.

Al concluir esta clase, tendrás un entendimiento claro de qué son las tuplas, cómo y cuándo utilizarlas en tus programas, y las prácticas recomendadas para trabajar con este tipo de datos inmutable. Las tuplas son una herramienta poderosa en Python, y saber cómo utilizarlas te permitirá escribir código más seguro y eficiente.

----

Ciertamente se parecen mucho a las listas, teniendo una estructura semejante en este caso su declaratorio no es con corchetes cuadrados `[ ]` sino con paréntesis `( )`, son otra estructura de datos que almacenan una secuencia de elementos pero en este caso estos elementos son inmutables, si desearamos cambiar este tipo de datos nos reflejaria como error.

Vamos a ver ejemplo practico a continuación sobre las **Tuplas**:

```python
#!/usr/bin/python3

example = (1, 2, 3, 4, 5)

print(example[1:3])
```

Aquí podemos observar que de igual manera como en las listas podemos englobar un rango de elementos sobre la lista o tuplas en este caso.

Pero ahora veremos si tratamos de cambiar el tipo de datos dentro de la tupla no nos permitirá:

```python
#!/usr/bin/python3

example = (1, 2, 3, 4, 5)

example[0] = 8
```

Al intentar ejecutar este comando por consola nos reflejara como error.

Dentro de las tuplas al igual que las listas podemos agregar varios elementos, entre ellos una cadena, una lista, valores boolenaos, etc.

```python
#!/usr/bin/python3

example = (1, "test", [1, 2, 3], 4, True, {'manzanas': 1, 'peras': 5}, 5)

for element in example:
	print(element)
```

De igual manera podemos crear tuplas que contengan listas y listas que contengan tuplas.

En las Tuplas no tenemos la opción de usar las funciones como `insert()`, `extend()`, `remove()`, `append()`, `pop()` como lo hacíamos con las listas, todas estas funciones no son funcionales ya que las tuplas son inmutables

Ahora mostraremos un ejemplo donde si queremos recibir elementos de esta tupla y asignarle algunas variables lo podemos hacer de esta manera cómoda donde podemos igualar los valores a, b, c, d a `mi_tupla` de forma de que cada elemento de esta variable se convierta en cada una de las variables a, b, c, d 

listando la información de la siguiente manera:

```python
#!/usr/bin/python3

mi_tupla = (1, 2, 3, 4)

a, b, c, d = mi_tupla

print(a)
print(b)
print(c)
print(d)
```

A pesar de que no podemos alterar una tupla de manera directa, si lo podemos hacer de manera indirecta:

```python
#!/usr/bin/python

mi_primera_tupla = (1, 2, 3, 4)
mi_segunda_tupla = (5, 6, 7, 8, 9)

mi_tercera_tupla = mi_primera_tupla + mi_segunda_tupla

print(mi_tercera_tupla)
```

Para duplicar los elementos de la tupla principal lo podemos hacer con el símbolo `*`

```python
#!/usr/bin/python

mi_primera_tupla = (1, 2, 3, 4)
mi_segunda_tupla = (5, 6, 7, 8, 9)

mi_tercera_tupla = mi_primera_tupla*3

print(mi_tercera_tupla)
```

también podemos identificar números pares, recuerden que siempre que quieran modificar las tuplas van a tener que crear otra nueva tupla que almacene esos nuevos valores

Primero queremos iterar por cada uno de los elementos con `for i in mi_tula` para almacenar todos los valores en `i` asi que listamos con `i` al inicio pero siempre y cuando se cumpla una función entonces agregamos el `if i % 2 == 0` para cuando divida para `2` su resultado sea y finalmente convertimos todo esto en una `tupla`:

```python
#!/usr/bin/python

mi_primera_tupla = (1, 2, 3, 4, 5, 6, 7, 8, 9)

numeros_pares = tuple(i for in mi_tupla if i % 2 == 0)

print(numeros_pares)
```

Y si cambiamos el valor de `0` a `1` nos mostraría todos los números impares

¿En qué escenarios prácticos esta esto representado para que cobre sentido el porqué no se puedan alterar estos elementos de la tupla a diferencia de las listas ?

En este ejercicio imaginaremos que tenemos un ejemplo práctico con una base de datos creadas con tuplas con usuarios y contraseñas de la siguiente manera:

```python
#!/usr/bin/python3

db1_credencial = ("chemaAlonso", "chema123")
db2_credencial = ("Hacker", "hacker123")

try:
	db1_credential[0] = "Manolo"
except TypeError:
	print("No es posible manipular los elementos de una tupla")
```

Tengan en cuentan los conceptos practicos de tuplas que se parecen mucho a las listas a difencia de los corchetes por los parentesis, que sus elementos son inmutables y se pueden realizar operaciones con estas con varias tuplas 