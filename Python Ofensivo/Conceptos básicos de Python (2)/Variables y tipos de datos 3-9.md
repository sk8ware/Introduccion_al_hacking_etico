
----
- TAG: #Python #Programación #Cadenas #Listas #TypeCasting #Bucles
- ----
Las variables en Python son como nombres que se le asignan a los datos que manejamos. Piensa en una variable como un nombre que pones a un valor, para poder referirte a él y utilizarlo en diferentes partes de tu código.

En la clase actual, vamos a enfocarnos en comprender las variables y algunos de los tipos de datos fundamentales en Python. Estos conceptos son esenciales, ya que nos permiten almacenar y manipular la información en nuestros programas.

**Variables**

Una variable en Python es como un nombre que se le asigna a un dato. No es necesario declarar el tipo de dato, ya que Python es inteligente para inferirlo.

**Cadenas (Strings)**

Las cadenas son secuencias de caracteres que se utilizan para manejar texto. Son inmutables, lo que significa que una vez creadas, no puedes cambiar sus **caracteres individuales**.

**Números**

Python maneja varios tipos numéricos, pero nos centraremos principalmente en:

- **Enteros (Integers)**: Números sin parte decimal.
- **Flotantes (Floats)**: Números que incluyen decimales.

**Listas**

Las listas son colecciones ordenadas y mutables que pueden contener elementos de diferentes tipos. Son ideales para almacenar y acceder a secuencias de datos.

Y para trabajar con estas listas, así como con cadenas y rangos de números, utilizaremos los bucles ‘**for**‘, que nos permiten iterar sobre cada elemento de una secuencia de manera eficiente.

Estas son solo algunas de las estructuras de datos con las que trabajaremos por el momento. A medida que avancemos en las próximas clases, exploraremos más tipos de datos y estructuras más complejas, ampliando nuestras herramientas para resolver problemas y construir programas más sofisticados.

-----
Vamos a empezar por la cadenas 

Para ello vamos a empezar creando un archivo `example.py` donde agregaremos lo siguiente
```python
#!/usr/bin/python3

cadena = "Mi cadena"

print(cadena)
```

Ahora salimos de consola y lo ejecutamos con `python3` para ver la respuesta por consola 
```python
python3 exmaple.py
```

Salida esperada:
`Mi cadena`

Como es una variable ahora le podriamos cambiar por una dirección ip y usar la regla `snake_case` 
```python
#!/usr/bin/python3

ip_adress = "123.45.678.90"

print(ip_adress)
```

Si queremos ver el tipo de dato lo podemos de imprimir agegrandole el siguiente print
```python
#!/usr/bin/python3

ip_address = "123.45.678.90"

print(ip_address)
print(type(ip_address))
```

Y podemos observar que en la salida no nos sale como tipo de número entero, sino como `class 'str'` 
Si deseamos que nos aparezca como número enteros tenemos que realizarlo de la siguiente manera
```python
#!/usr/bin/python3

port = 80 
print(port)
print(type(port))
```

Aqui de esta manera si encontraremos el numero como entero en la respuesta en consola con `class'int'` 

Ahora con el ejemplo `float` que significa **floating point** que es una representación númerica que puede manejar números reales, es decir un número que tiene una parte decimal 

```python
#!/usr/bin/python3
number = 4.5
print(number)
print(type(number))
```

En esta salida por lo general esperaríamos una respues de clase `class'float'`

Ahora hablaremos del **Type Casting**  que nos permite para la conversión de datos de int a float
```python
#!/usr/bin/python3
number = float(4)
print(number)
print(type(number))
```

y tendremos de respuesta que es `4.0` y de tipo `float` 

4.0
<class 'float'>

Ahora veremos un poco sobre las **LISTAS** que son una estructura de datos que nos permiten almacenar multiples elementos en un mismo contenedor, cada elemento puede ser accedido o consultados mediantes unos indices, creamos un ejemplo a continuación:
```python
#!/usr/bin/python3

my_ports = []
my_ports.append(22)
my_ports.append(80)
my_ports.append(443)

print(my_ports[0])
print(my_ports[1])
print(my_ports[2])
``` 

Esta sería una de las manera que **NO** hay que utilizar ya que seria una manera incorrecta de hacerlo 

Una de las maneras para poder reducir esto seria de la siguiente manera, utilizando un bucle `for` 
```python
#!/usr/bin/python3

my_ports = []
my_ports.append(22)
my_ports.append(80)
my_ports.append(443)

for port in my_ports:
	print(port)
```

Asi de esta  manera no nos preocupamos por saber cuantos datos exista ya que emprimira todo

Por ejemplo si quisieramos integrar una cadena con la respuesta por consola lo podemos realizar de la siguiente manera
```python
#!/usr/bin/python3

my_ports = []
my_ports.append(22)
my_ports.append(80)
my_ports.append(443)

for port in my_ports:
	print("Puerto: " + str(port))
```

o tambien se puede hacer con `f`
```python
for port in my_ports:
	print(f"Puerto: {port}")
```
Tomen en cuenta que dentro del buqle pueden agregar mas instrucciones pero tienen que estar bien tabulados
```python
for port in my_ports:
	print(f"Puerto: {port}")
print(f"\n[+] La lista tiene un total de: {len(my_ports)} elementos")
```

>Esta seria la manera incorrecta de hacerlo, ya muchas veces pensamos mal al momento de tener logica en el codigo
```python
#!/usr/bin/python3

my_ports = []
my_ports.append(22)
my_ports.append(80)
my_ports.append(443)

for port in my_ports:
	print("Puerto: " + port)
```

# Ahora veremos la forma mas optima de hacerlo

Borramos todos los my_ports.append() y le agregamos todos los datos si lo sabemos de memoria o no hay nada contemplado
```python
#!/usr/bin/python3
my_ports = [22, 80, 433]

for port in my_ports:
	print(f"Puerto: {port}")
print(f"\n[+] La lista tiene un total de: {len(my_ports)} elementos")
```

La forma en la que podríamos agregar mas datos en la respuesta
 ```python
 #!/usr/bin/python3
 my_ports = [22, 80, 433]
 
 my_ports.extend([84, 85])

 for port in my_ports:
 	 print(f"Puerto: {port}")
 print(f"\n[+] La lista tiene un total de: {len(my_ports)} elementos")
 ``` 

O agregando la funcion 
```python
my_ports += [86, 87]
```

Aqui vamos a pedir que la respuesta sea my_ports pero sumandole 86 y 87 
```python
my_ports = my_ports + [86, 87]
```

Pero si imprimimos tendremos un resultado en desorden, para ello lo podremos solucionar con `.sorted` 
```python
#!/usr/bin/python3

 my_ports = [22, 80, 433]
 
 my_ports.extend([84, 85]) 

 my_ports = sorted(my_ports)
 
 for port in my_ports:
 	 print(f"Puerto: {port}")
 print(f"\n[+] La lista tiene un total de: {len(my_ports)} elementos")
```


# Para eliminar elementos de una lista

Para poder eliminar un elemento de una lista podemos utilizar la siguiente función, recuerden siempre que se empieza contando desde el indice 0 
```
del my_ports[0] 
```
----
# Practicando en la consola interactiva de python

Iniciamos Python desde nuestra consola
```zsh
python3
```

y realizamos el siguiente ejercicio:
```python
>>> mi_lista = [1, 2, 3, 4, 5]
>>> mi_lista
>>> [1, 2, 3, 4, 5]
```

Vemos que al crear la lista y ejecutarla no fue necesario escribir un `print` 

Ahora podemos seleccionar la cantidad de numeros o datos se impriman por pantalla
```python
>>> mi_lista[:2]
[1, 2]
```

O si solo deseamos seleccionar uno en especificio seria sin los dos puntos `:`
```python
>>> mi_lista[3]
[4]
```

Si utilizamos un rango por ejemplo de `[0:3]`  solo le estamos pidiendo que nos imprima un rango de 3 numeros y hace omiso al ultimo número que seria el 4
```python
 >>> mi_lista[0:3]
[1, 2, 3]
```

Pero si realizamos el siguiente ejemplo tan solo nos mostrara dos números ya que al ultimo número le resta uno
```
>>> mi_lista[2:4]
[3, 4]
```

Ahora para eliminar solo los elementos de izquierda podemos hacer lo siguiente
```
>>> mi_lista[2:]
[3, 4, 5]
```

O realizarlo al reves con `[:3]` 

Ahora si hacemos un si queremos mostrar un numero o del lado contrario
```python
>>> mi_lista[1]
2
```
```python
>>> mi_lista[-1]
5
```

Con `[-2:]` para mostrar para mostrar desde el numero 2 teniendo en consideración que se cuenta desde 0 
```python
>>> mi_lista[-2:]
[4, 5]
```

Recuerden que cuando se agrega el `-` y se cuenta desde el final el `0` no cuenta 

Tambien tenemos la opción de que cuando le agregamos la función `.insert` cambia la posición del primer númerp o el segundo número que ingresemos, también se lo puede sustituir por palabras
```
mi_lista.insert(2,9)
```

Si deseamos eliminar el ultimo número en especifico podemos usar la función  `pop`
```
mi_lista.pop()
```

Si deseamos saber que en que posición nos ubicamos lo podemos hacer con la función `index` 
```python
>>> mi_lista
[1, 2, 9, 3, 4, 5]
>>> mi_lista.index(9)
2
```

Si solemos tener numeros repetidos siempre lo toma en cuenta al primer numero que encuentre en la linea, siempre va de prioridad con el primer numero que se encuentre 

Si deseamos enumerar nuestras indices con un bucle, para que la primera parte que pertenece al indice pertenezca a `x` y lo que son los numeros en la variable `y` 
```python
>>> for x, y in enumerate(mi_lista):
...     print(x)
... 
0
1
2
3
4
5
```

Y con `y` seria la siguiente respuesta
```python
>>> for x, y in enumerate(mi_lista):
...     print(y)
... 
1
2
9
3
4
5
```

Para la creación de indices y que nos muestre el valor `12` representado en todos los valores podriamos utilizar la siguiente función
```python
indices = [x for x, y in enumarate(mi_lista) if y == 12]
```


Con `.count` podemos saber cuantas veces sale repetidas el mismo número
```
mi_lista.count(12)
```

Lo podrían imprimir de la siguiente manera para verlo de mejor manera esteticamente 
```
mi_lista(f"[+]Mi lista tiene un total{mi_lista.count(12)} elementos")
```

En listas se puede realizar el siguiente comando para saber que números se encuentran repetidos y luego hharemos que no exista archivos repetidos
```
mi_lista = sorted(mi_lista)
```

Volvemos a imprimir nuestra variable y se mostrará todo muy bien organizado, si vemos números repetidos sencillamente las eliminamos con el siguiente comando
```
set(mi_lista)
```

Este ejemplo se puede aplicar tanto este organizado o no, se puede practicar de varias maneras agregando numeros en desorden y tratar de eliminar los números repetidos.

Se puede imprimir el número mas alto de la siguiente manera con la función `max`
```python
print(f"[+]El número mas alto es: {max(mi_lista)}")
```

O si desean ver el mínimo sería con `min`

Para sumar los valores de mi_lista podemos realizarlo de la siguiente manera
```
sum(mi_lista) / len(mi_lista)
```

