
---
- TAG:
-----
Los conceptos vistos en esta clase son esenciales para entender cómo crear programas en Python que puedan tomar decisiones y repetir acciones hasta cumplir ciertos criterios. Aquí es donde nuestros programas obtienen la capacidad de responder a diferentes situaciones y datos.

**Condicionales**

Los condicionales son estructuras de control que permiten ejecutar diferentes bloques de código dependiendo de si una o más condiciones son verdaderas o falsas. En Python, las declaraciones condicionales más comunes son ‘**if**‘, ‘**elif**‘ y ‘**else**‘.

- **if**: Evalúa si una condición es verdadera y, de ser así, ejecuta un bloque de código.
- **elif**: Abreviatura de “**else if**“, se utiliza para verificar múltiples expresiones sólo si las anteriores no son verdaderas.
- **else**: Captura cualquier caso que no haya sido capturado por las declaraciones ‘**if**‘ y ‘**elif**‘ anteriores.

**Bucles**

Los bucles permiten ejecutar un bloque de código repetidamente mientras una condición sea verdadera o para cada elemento en una secuencia. Los dos tipos principales de bucles que utilizamos en Python son ‘**for**‘ y ‘**while**‘.

- **for**: Se usa para iterar sobre una secuencia (como una lista, un diccionario, una tupla o un conjunto) y ejecutar un bloque de código para cada elemento de la secuencia.
- **while**: Ejecuta un bloque de código repetidamente mientras una condición específica se mantiene verdadera.

**Control de Flujo en Bucles**

Existen declaraciones de control de flujo que pueden modificar el comportamiento de los bucles, como ‘**break**‘, ‘**continue**‘ y ‘**pass**‘.

- **break**: Termina el bucle y pasa el control a la siguiente declaración fuera del bucle.
- **continue**: Omite el resto del código dentro del bucle y continúa con la siguiente iteración.
- **pass**: No hace nada, se utiliza como una declaración de relleno donde el código eventualmente irá, pero no ha sido escrito todavía.

En esta clase, profundizaremos en cada uno de estos aspectos con ejemplos detallados. Aprenderemos cómo tomar decisiones dentro de nuestros programas y cómo automatizar tareas repetitivas. Esto nos dará la base para escribir programas que pueden manejar tareas complejas y responder dinámicamente a los datos de entrada. Al final de la clase, estarás equipado con el conocimiento para controlar el flujo de tus programas de Python de manera eficiente y efectiva.

----
Vamos primero por los `bucles y los condicionales`

# Bucles
Los bucles nos permiten iterar sobre una secuencia, pueden ser tanto como duplas, diccionarios, conjuntos etc
Para explicarlo de mejor manera y detallado vamos a realizarlo con el siguiente ejercicio
```python
#!/usr/bin/python3
for pepito in range(5):
	print(pepito)
```
Salida:
❯ python3 test.py
0
1
2
3
4

En este caso mostrará la respuesta 01234 ya que cuando especificamos rangos para englobar o elementos de una lista, siempre suele la cantidad que especificamos menos el ultimo número ya que cuenta siempre desde el 0  

Ahora veremos otro ejemplo agregando variables;
```python
#!/usr/bin/python3

names = ["sk8ware", "Marcelo", "TheGodHacker"]

for name in names:
    print(f"El nombre para esta vuelta es{name}")
```

Ahora utilizaremos la función `while` para poder dar un pequeño ejemplo y puedan ver las diferencias entre la creación de bucles con diferentes funciones
```python
#!/usr/bin/python3

i = 0 

while i < 5:
	print(i)
	
	i += 1 
```

Depende de la instrución que le indiquemos cumplira la función pero si no se indica la instrución while sería un bucle infinito 


Otra forma de jugar es con `Enumerate` 
```python
#!/usr/bin/python3

nombres = ["Pepe", "Mitis", "Claudia", "Negra"]

for contador, nombre in enumerate(nombres):
	print(f"Nombre [{contador+1}]: {name}")
```

Recuerden que enumerate siempre devuelve el indice y el valor
Va retornando tanto el indice como el valor 
para ello hay que separarlo en dosvariables
y el {i+1} permite que no cuente desde 0 y muestre desde 1 


Otro ejemplo podria ser la implementación de diccionarios junto con bucles
En resume los diccionarios son una estrucutura de datos no ordenados que almacen pares de clave valor 
ejemplo:
```python
#!/usr/bin/python3

frutas = {"sandia": 4, "manzana": 5, "melon": 8}

for fruta, cantidad in frutas.items():
    print(f"Hay {cantidad} cantidades de la fruta {fruta}")
```

Ahora tendremos los bucles anidados

Esto seria una forma muy chula de hacer bucles dentro de otros bucles, para ello vamos a crear una lista sobre otra lista

```python
#!/usr/bin/python3

my_list = [[1, 4, 5], [2, 6, 8], [9, 4, 1]]

for element in_list:
	
	print(element)
```


Para desglozarlo lo podriamos hacer de la siguiente manera
```python
#!/usr/bin/python3

my_list = [[1, 4, 5], [2, 6, 8], [9, 4, 1]]

for element in my_list:
	for element_in_list in element:
		print(element)
```

Le podemos añadir un poco de estita para verlo de mejor manera en la salida por consola
```python
#!/usr/bin/python3

my_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

for element in my_list:
    print(f"\n[+] Vamos desglosar la lista{element}\n")
    for element_in_list in element:
        print(element_in_list)
```

Para iterar sobre esta lista se usa `element_in_list` 

Otra forma que tuvieras de jugar con bucles sobre una lista es hacer como se conoce una lista de comprensión (for)
creando el ^ de cada numero 
```python
#!/usr/bin/python3
odd_list = [1, 3, 5, 7, 9]
cuadrado = [i ** 2 for i in odd_list]

print(cuadrado)
```

Tambien tenemos una opción que nos permite cortar hasta cierto limite que nosotros queramos con la función `break` 
Hay que tomar en cuenta la importancia de la colocación del `print` ya que segun la posición mostrara uno u otra respuesta
```python
#!/usr/bin/python3

for i in range(10):

	if i == 5:
		break
		
	print(i)
```

o 

```python
#!/usr/bin/python3

for i in range(10):
	print(i)
	
	if i == 5:
		break
```

Aliada a `break` tambien hay la utilllidad en bucles que es `continue` cuando no queramos que pase nada en concreto 
```python
#!/usr/bin/python3

for i in range(10):
	
	if i == 5:
		continue
	print(i)
```

Asi mismo cuando hablamos de condicionales una cosa es el `if` y otra cosa el `else` que es lo que define como lo contrario a la condición
```python
#!/usr/bin/python3

for i in range(10):

	if i ==5:
		print("Actualmente 'i' vale 5")
	else:
		print("Actualmente 'i' no vale 5")
```

Si solo tuvieramos la opción `if` nos mostraria solo la respuesta de lo que vale if, pero si agregamos la función `else` para que muestre lo que vale los demas números dentro de `range(10)`

```python
#!/usr/bin/python3

for i in range(10):

    if i == 5:
        print("Actualmente el valor de 'i' es 5")
    else: 
        print("Actualmente el valor de 'i' no es de 5")

```

Si desean ver el numero al que pertenece simplemente le agregan al final del 5 la función `[{i}]` y la `f` antes de las comillas del principio 