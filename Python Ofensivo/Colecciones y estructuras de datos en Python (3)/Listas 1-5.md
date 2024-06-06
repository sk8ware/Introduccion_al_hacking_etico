
----
- TAG: - #python #listas #estructurasdedatos
---
En esta clase, nos sumergiremos en profundidad en uno de los tipos de datos más versátiles y utilizados en Python.

Las listas son estructuras de datos que nos permiten almacenar secuencias ordenadas de elementos. Son mutables, lo que significa que podemos modificarlas después de su creación, y son dinámicas, permitiéndonos añadir o quitar elementos de ellas.

**Características de las Listas**

Vamos a explorar las características clave de las listas en Python, que incluyen su capacidad para:

- Almacenar datos heterogéneos, es decir, pueden contener elementos de diferentes tipos (enteros, cadenas, flotantes y más) dentro de una misma lista.
- Ser indexadas y cortadas, lo que permite acceder a elementos específicos de la lista directamente a través de su índice.
- Ser anidadas, es decir, una lista puede contener otras listas como elementos, lo que permite crear estructuras de datos complejas como matrices.

**Operaciones con Listas**

También cubriremos las operaciones fundamentales que se pueden realizar con listas, como:

- Añadir elementos con métodos como ‘**append()**‘ y ‘**extend()**‘.
- Eliminar elementos con métodos como ‘**remove()**‘ y ‘**pop()**‘.
- Ordenar las listas con el método ‘**sort()**‘ o la función incorporada ‘**sorted()**‘.
- Invertir los elementos con el método ‘**reverse()**‘ o la sintaxis de corte ‘**[::-1]**‘.
- Comprender las comprensiones de listas, una forma “pythonica” de crear y manipular listas de manera concisa y eficiente.

**Métodos de Listas**

Profundizaremos en la rica gama de métodos que Python ofrece para trabajar con listas y cómo estos métodos pueden ser utilizados para manipular listas de acuerdo a nuestras necesidades.

**Buenas Prácticas**

Discutiremos las mejores prácticas en el manejo de listas, incluyendo cómo y cuándo usar listas en comparación con otros tipos de colecciones en Python, como tuplas, conjuntos y diccionarios.

Al final de esta clase, tendrás un conocimiento profundo de las listas en Python y estarás equipado con las técnicas para manejarlas eficazmente en tus programas. Con esta base sólida, podrás manipular colecciones de datos con confianza y aplicar esta habilidad central en tareas como la manipulación de datos, la automatización y el desarrollo de algoritmos.

---
# Listas 

Las listas como tal es una estructura de datos mutables ya que se pueden alterar sus elementos

Vamos a repasar un poco con los siguientes elementos:

```python
#!/usr/bin/python3

puertos_tcp = [21, 22, 25, 80, 443, 8080, 445, 69]

puertos_tcp.append(1337)

print(len(puertos_tcp))

```

En este ejemplo creamos una lista y agregamos un valor extra con `.append(1337)` y la función `len()` nos permite enumerar cuantos valores o contenido tenemos en la lista 

Recuerden que se pueden crear bucles para correr elemento por elemento y efectuar una operatoria en cada uno es estos 

Lo podemos emplear de la siguiente manera agregando con la función `print(f"")` 

```python
#!/usr/bin/python3

puertos_tcp = [21, 22, 25, 80, 443, 8080, 445, 69]

puertos_tcp.append(1337)

for puerto in puertos_tcp:
	print(f"Este es el puerto {puerto}")
```

Ahora con otro ejemplo práctico podemos utilizar de ejemplo las vulneravilidades

```python
#!/usr/bin/python3

cve_list = ['CVE-2023-1435', 'CVE-2022-45761', 'CVE-2023-7863']

print(cve_list)
cve_lis.remove('CVE-2023-7863')
print(cve_list)
```

Aquí podremos ver que tenemos un lista con tres valores que con la función `remove()` y al volver a imprimir después de esta función nos mostrará la lista sin el elemento seleccionado para eliminar.

También podemos ordenar las listas de la siguiente manera con el anterior ejercicio para que nos muestre de menos a mayor número utilizando `.sort()`

```python
#!/usr/bin/python3

puertos_tcp = [21, 22, 25, 80, 443, 8080, 445, 69]

puertos_tcp.append(1337)

puertos_tcp.sort()

print(puertos_tcp)
```

Asimismo, podemos invertir el orden con `.reverse`, practicando con otro ejercicio sencillo con ataques de ciberseguridad:

```python
#!/usr/bin/python3

attacks = ['Pishing', 'DDos', 'SQL Injection', 'Man in the middle', 'Cross-site Scripting']

print(attacks)

attacks.reverse()

print(attacks)
```

Si deseamos acceder a cada elemento de la lista lo podemos realizar de la siguiente manera:

```python
#!/usr/bin/python3

attacks = ['Pishing', 'DDos', 'SQL Injection', 'Man in the middle', 'Cross-site Scripting']

primer_ataque = attacks[2]

print(primer_ataque)
```

Recuerden que podemos manipular diferentes funciones entre los corchetes para elegir la cantidad de datos que deseemos. Cuando el número es negativo, representa la eliminación de datos contando desde el final y empezando desde el número `1` a diferencia de lo normal que se suele contar desde `0`. Siempre que se pongan los dos puntos, comenzará el conteo desde 1.
- [:3]
- [:-3]
- [3:]
- [-1]

Intenten practicar lo más que puedan con estos ejercicios para comprender mejor cómo nos ayudan a demostrar contenido. Antes de los dos puntos `:`, muestra todos los elementos después del número indicado. Por ejemplo, si el `1` mostraría los datos después de Phishing, comenzando desde DDoS. A diferencia de poner el número a la derecha después de los dos puntos, muestra únicamente el valor o los valores indicados. En este caso, si es el `1`, mostraría tan solo el primer dato que sería Phishing.

Como también hemos practicado con los bucles **While** podemos crear un bucle de la siguiente manera:

Declaramos un variable que valga `i` que valga cero `0` que representará como nuestro contador y mientras `i` sea igual a la longitud de elementos, para que muestre todos los elementos existentes, para ello necesitamos imprimir attacks en esa posición de índice, de manera que hacemos que el valor `i` valga un número nuevo cada vuelta, le agregamnos este valor ya que por lo normal imprimiría hasta el penúltimo valor  ya que cuenta desde 0 y no llegaría a 5, por eso le agregamos el `i += 1`

```python
#!/usr/bin/python3

attacks = ['Pishing', 'DDos', 'SQL Injection', 'Man in the middle', 'Cross-site Scripting']

i =0 # Contador

while i < len(attacks):
	print(attacks[i])
	i += 1
```

También tenemos la forma **Enumerate** para cuando queramos recibir el índice y el valor del elemento correspondiente:

Creamos una función `for` con el valor `i` para el índice y `attack` para `enumerate`, que nos regresa un índice y el valor de esa lista iterable que se está recorriendo.

```python
#!/usr/bin/python3

attacks = ['Pishing', 'DDos', 'SQL Injection', 'Man in the middle', 'Cross-site Scripting']

for i, attack in enumerate(attacks):
	print(f"Para la posicisión {i+1} tendríamos el ataque {attack}")

```


Ahora, imaginen que deseamos convertir todas las minúsculas en mayúsculas. Podríamos hacerlo de la siguiente manera con la función `.upper()`:

Creamos una nueva lista e iteramos por cada elemento para que todo se convierta en mayúsculas.

```python
#!/usr/bin/python3

attacks = ['Pishing', 'DDos', 'SQL Injection', 'Man in the middle', 'Cross-site Scripting']

attacks_uppercase = [attacks.upper() for attack in attacks]

print(attacks_uppercase)
```

De igual manera, para convertir todas las letras mayúsculas a minúsculas, podemos hacerlo de la siguiente manera con la función `.lower()`:

```python
#!/usr/bin/python3

attacks = ['Pishing', 'DDos', 'SQL Injection', 'Man in the middle', 'Cross-site Scripting']

attacks_uppercase = [attacks.lower() for attack in attacks]

print(attacks_uppercase)

```

Ahora mostraremos como podríamos hacer para poder combinar las listas:

Utilizaremos la función `zip` para que cuando le pasemos los valores iterables nos lo muestre con la edad después de dos puntos :

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']
edades = ['25', '25', '33', '48']

for nombre, edad in zip(nombres, edades):
	print(f"{nombre} tiene {edad} años") 
```

Para eliminar en este tipo de listas, solemos utilizar `del`:

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']

del nombres[2]

print(names)
```

Otra manera de eliminar es `remove`, para no complicarte leyendo en listas más grandes y perderte entre tantos elementos. Lo podemos simplificar de la siguiente manera:

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']

nombres.remove("Pedro")

print(nombres)
```

Si deseamos limpiar toda la lista, usamos `.clear`:

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']

nombres.clear()

print(nombres)
```

Hay ocasiones en que queremos quitar un elemento de la lista y almacenarlo en una variable. Esto es posible con la herramienta `.pop`, que elimina el último elemento de la lista:

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']

nombres.pop()

print(nombres)
```

Si lo ejecutamos en repetidas ocasiones, seguirá eliminando siempre el último elemento:

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']

nombres.pop()
nombres.pop()

print(nombres)
```

Pero al eliminarlo, también podemos moverlo a una variable que nos indique que fue eliminado:

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']

usuario_eliminado = nombres.pop(2)

print(nombres)
print(f"El usuario eliminado a sido {usuario_eliminado}")
```

Como mencioné al inicio, las listas son mutables y podemos cambiar su contenido por la posición en la que se encuentren, con el mismo nombre de la variable y asignando el número en el que se encuentran ubicados:

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']

nombres[2] = "Silvia"

print(nomrbes)
```

ambién podemos agregar otro elemento en una posición específica utilizando la función `.insert`:

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']

nombres.insert(2, "Silvia")

print(nomrbes)
```

En caso de tener varias listas, podemos combinarlas de la siguiente manera con la función `.extend()`:

```python
#!/usr/bin/python3

nombres = ['Anthony', 'Claudia', 'Pedro', 'David']
otros_nombres = ['Juan', 'Carlos']

nombres.extend(otros_nombres)
print(nombres)
```