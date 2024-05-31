
-----
- TAG: 
-----
En esta clase nos sumergimos en dos conceptos fundamentales de la programación en Python que potencian la modularidad y la gestión eficaz de los datos dentro de nuestros programas.

**Funciones**

Las funciones son bloques de código reutilizables diseñados para realizar una tarea específica. En Python, se definen usando la palabra clave ‘**def**‘ seguida de un nombre descriptivo, paréntesis que pueden contener parámetros y dos puntos. Los parámetros son “**variables de entrada**” que pueden cambiar cada vez que se llama a la función. Esto permite a las funciones operar con diferentes datos y producir resultados correspondientes.

Las funciones pueden devolver valores al programa principal o a otras funciones mediante la palabra clave ‘**return**‘. Esto las hace increíblemente versátiles, ya que pueden procesar datos y luego pasar esos datos modificados a otras partes del programa.

**Ámbito de las Variables (Scope)**

El ámbito de una variable se refiere a la región de un programa donde esa variable es accesible. En Python, hay dos tipos principales de ámbitos:

- **Local**: Las variables definidas dentro de una función tienen un ámbito local, lo que significa que solo pueden ser accesadas y modificadas dentro de la función donde fueron creadas.
- **Global**: Las variables definidas fuera de todas las funciones tienen un ámbito global, lo que significa que pueden ser accesadas desde cualquier parte del programa. Sin embargo, para modificar una variable global dentro de una función, se debe declarar como global.

Durante esta clase, exploraremos cómo definir y llamar funciones, cómo pasar información a las funciones a través de argumentos, y cómo las variables interactúan con diferentes ámbitos. También veremos las mejores prácticas para definir funciones claras y concisas y cómo el correcto manejo del ámbito de las variables puede evitar errores y complicaciones en el código.

Comprender estos conceptos es esencial para escribir programas claros, eficientes y mantenibles en Python. Al finalizar la clase, tendrás una sólida comprensión de cómo estructurar tu código y cómo gestionar las variables para que tus programas funcionen de manera impecable.

----
# Funciones y  ámbito de las variables

Estos son temas muy importantes que vamos a estar viendo muy seguido en el resto del bloc de notas

# Funciones

Como ya hemos explicado lo teórico, vamos a empezar con lo práctico con el siguiente ejemplo 
Son bloques de codigo que son reusables y que realizan una tarea en especifico
```python
#!/usr/bin/python3

def saludo():
    print("\n¡Hola mundo!")

saludo()

```

# def

Significa  `define` que nos permite **definir** algo, como la función demostrada
Le definimos un **hola mundo** con `print` 
Lo comodo de las funciones es que podemos asignar el nombre que nosotros queramos, pasandole a la función un argumento, y la variable "nombre" cambiaría a valer el nombre "Manuel" en la parte de **saludo**

```python
#!/usr/bin/python3

def saludo(nomrbe):
    print(f"\n¡Hola {nombre}!")

saludo("Manuel")
```

La particularidad de las funciones es que pueden retonar cosas
Imaginen que `saludo` lo cambiamos a `suma` y le vamos a pasar dos valores 2,8 deseando que el resultado sea la suma de ambos valores, poniendo en una variable que se llame   `resultado` para luego obtener un resultado con la función `print` jugando con **f-string**, ahora debemos declarar las variables `x, y` y ahora como nos va a devolver un resultado, asi que nos tiene que retornar algo y con eso lo hacemos con `return` nos devuelva `x + y` para que 2 valga x y 8 valga y
```python
#!/usr/bin/python3

def suma(x,y):
	return x + y

resultado = suma(2, 8)

print(f"\n[+] La suma de ambos valores es {resultado}")
```


# Ámbito de las variables 

Imagen que tenemos la función `mi_funcion()` y definimos una variable `variable_local`, asi que si hacemos un `print`de esta variable, asi que llamamos a esta función con `mi_funcion()`
```python
#!/usr/bin/python3

def mi_funcion():
	variable_local = "Soy una variable local"
	print(variable_local)

mi_funcion()
```


En este caso la variable `variable_local` únicamente existe bajo el contexto de la propida definición de la función, internamente claro?
Pero afuera no es accesible
Por eso es muy diferente cuando definimos una **variable global**, de la siguiente manera podríamos agregar una variable global 

```python
#!/usr/bin/python3

variable_global = "Soy una variable global"

def mi_funcion():
	print(variable_global)

mi_funcion()

print(variable_global)
```

Muy distinto si nosotros aqui le agregamos la función `global variable`  ya que cambia todo el panorama
```python
#!/usr/bin/python

variable = "Soy global"

def mi_funcion():
	global variable
	variable = "Soy global y he sido modificado"
	print(variable)
mi_funcion()

print(variable)
```
