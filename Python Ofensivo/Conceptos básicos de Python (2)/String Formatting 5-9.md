
----
- TAG:
-----
Python proporciona varias maneras de formatear cadenas, permitiendo insertar variables en ellas, así como controlar el espaciado, alineación y precisión de los datos mostrados. Aquí están las técnicas de formateo de cadenas que exploraremos:

**Operador % (Porcentaje)**

También conocido como “i**nterpolación de cadenas**“, este método clásico utiliza marcadores de posición como ‘**%s**‘ para cadenas, ‘**%d**‘ para enteros, o ‘**%f**‘ para números de punto flotante.

**Método format()**

Introducido en Python 2.6, permite una mayor flexibilidad y claridad. Utiliza llaves ‘**{}**‘ como marcadores de posición dentro de la cadena y puede incluir detalles sobre el formato de la salida.

**F-Strings (Literal String Interpolation)**

Disponible desde Python 3.6, los F-Strings ofrecen una forma concisa y legible de incrustar expresiones dentro de literales de cadena usando la letra ‘**f**‘ antes de las comillas de apertura y llaves para indicar dónde se insertarán las variables o expresiones.

En esta clase, nos enfocaremos en cómo utilizar cada uno de estos métodos para formatear cadenas efectivamente, así como las situaciones en las que cada uno podría ser más apropiado. Al final, tendrás las herramientas para presentar información de manera profesional en tus programas de Python.

----

Empezamos creando un archivo `test.py` y practicamos un poco con los siguientes ejercicios:
```python
#!/usr/bin/python3

name = "sk8ware"
print("Hola, mi nombre es " + name)
```

Esto nos daría como respuesta
```sh
Hola, mi nombre es sk8ware
```

Claro en este caso no nos representa algun error ya que ambos tipos son variables, pero si cambiaramos el tipo de texto 

 Si quisiera sustitutir  u organizar las variales las podríamos representar con `%s` que significa string
 ```python
#!/usr/bin/python3

name = "sk8ware"
rol = "lammer"

print("Hola, mi nombre es %s y soy un %s " % (name, rol))
```

En el caso de que queramos agregar números decimales lo podemos hacer de la siguiente manera agregando `%d` que significa **decimal**
```python
#!/usr/bin/python3

name = "sk8ware"
rol = "lammer"

edad = 25 

print("Hola, mi nombre es %s y soy un %s. Actualmente tengo %d años" % (name, rol, edad))
```

Aun que tambien hhubiese funcionado si le agregabamos la función `%s` pero es mejor declararlo en decimal para evitar errores

Tambien tenemos otra forma para poder demostrar este ejemplo de una manera mas simplificada 
```python
#!/usr/bin/python3

name = "sk8ware"
rol = "lammer"

edad = 25 

print("Hola, soy {}!".format(name))
print("Hola, soy {}! y tengo {} años".format(name, edad))
```

Se le puede agregar los indices dentro de las de 0 hacia delante `{0}`
```python
#!/usr/bin/python3

name = "sk8ware"
rol = "lammer"

edad = 25 

print("Hola, soy {}!".format(name))
print("Hola, soy {0}! y tengo {1} años. No es broma, mi nombre real es {0}".format(name, edad))
```

Otra forma de hacerlo es con las `f-strings` que se le agrega una `f` antes de las comillas y dentro de las llaves representar por `name`, es una de las maneras mas comodas con las cuales sustituir 
```python
#!/usr/bin/python3

name = "sk8ware"
rol = "lammer"

edad = 25 

print(f"Hola, soy {name}!")
print(f"Hola, soy {name}! y tengo {edad} años. No es broma, mi nombre real es {name}")
```
