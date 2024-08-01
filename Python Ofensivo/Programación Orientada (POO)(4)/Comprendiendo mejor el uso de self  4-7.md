
----
- TAG:
-----
El uso de self es uno de los aspectos más fundamentales y a la vez confusos para quienes se adentran en la Programación Orientada a Objetos (POO) en Python. Este identificador es crucial para entender cómo Python maneja los métodos y atributos dentro de sus clases y objetos.

**Definición de ‘self’**

A nivel conceptual, ‘**self**‘ es una referencia al objeto actual dentro de la clase. Es el primer parámetro que se pasa a cualquier método de una clase en Python. A través de self, un método puede acceder y manipular los atributos del objeto y llamar a otros métodos dentro del mismo objeto.

**Uso de ‘self’**

Cuando se crea una nueva instancia de una clase, Python pasa automáticamente la instancia recién creada como el primer argumento al método ‘**__init__**‘ y a otros métodos definidos en la clase que tienen self como su primer parámetro. Esto es lo que permite que un método opere con datos específicos del objeto y no con datos de la clase en general o de otras instancias de la clase.

**Importancia de ‘self’**

El concepto de self es importante en la POO ya que asegura que los métodos y atributos se apliquen al objeto correcto. Sin self, no podríamos diferenciar entre las operaciones y datos de diferentes instancias de una clase.

En esta clase, nos enfocaremos en comprender a fondo cómo y por qué self es usado en Python, explorando su papel en la interacción con las instancias de la clase. Desarrollaremos una comprensión clara de cómo self permite que las clases en Python sean intuitivas y eficientes, manteniendo un estado consistente a través de las operaciones del objeto. Este conocimiento es esencial para trabajar con clases y objetos de manera efectiva y aprovechar la potencia de la POO.

---

Vamos a praticar con un ejercicio empleando una clase para explicar de mejor manera el uso de `self`

Esta plantilla puede contener tanto métodos como atributos, recuerden que la clase no es un objeto, es cuando instanciamos la clase que creamos un objeto eso seria la instancia de la clase, esta clase tendria sus metodos y atributos que hayamos definido en la clase 

Se empieza creando un constructor `def __init__()`

Cuando creamos una instancia de la clase, al hacer esto le estaríamos pasando unos valores para poder crear este objeto, sus propiedades y atributos serían `("Anthony", 25)`

```bash
#!/usr/bin/python3

class Persona:
	def __init__()

anthony = Persona("Anthony", 25)
```

Como estamos creando este objeto debemos irlo construyendo, que seria primero el método especial que es el constructor `def __init__()`, asi que le agregamos un `self` que hace referencia a `anthony`

Ya que cuando creamos el objeto `anthony` los atributos `("Anthony", 25)` se vincula de alguna manera al objeto `anthony`

En el siguiente ejemplo se hara referencia `self` al objeto `anthony` donde nombre valdra a Anthony y edad a 25

```bash
#!/usr/bin/python3

class Persona:
	def __init__(self, nombre, edad): #Persona.__init__(anthony, nombre, edad)
		self.anthony = nombre # anthony.nombre = "Anthony"
		self.edad = edad # anthony.edad = 28

anthony = Persona("Anthony", 25)
```

Si trataramos de imprimir dicha función, veremos que no funcionará por que no le hemos indicado lo que queremos que nos muestre, para ello debemos agregarle una definición con `def`

```bash
#!/usr/bin/python3

class Persona:
	def __init__(self, nombre, edad): #Persona.__init__(anthony, nombre, edad)
		self.nombre = nombre # anthony.nombre = "Anthony"
		self.edad = edad # anthony.edad = 28

	def presentacion(self): #Persona.presentacion(anthony)
		print(f"Hola soy {self.nombre} y tengo {self.edad} años") #anthony.nombre #anthony.edad

anthony = Persona("Anthony", 25)
anthony.presentacion()
```

Para imprimir el nombre o hacer referencia a el, debemos agregarle el `marcelo.presentacion()` al final del def presemtacion

Agregando el `print` que nos permitira ver por consola el texto agregando el `{self.nombre}` y `{self.edad}`

Cuando definimos un metodo, ese metodo internamente, puede hacer a otro metodo que este incluido en la plantilla de la clase, para ello es igual necesario utilizar el metodo `self` para poder acceder a ese otro metodo, desde otro metodo 

Ahora les indicare otro ejemplo implementando una `Class` y de nombre `Calculadora`
Seguido del constructor `__init__()`
Creamos un objeto que se llame `calc` con el valor de `(5)`, Este seria el número con el que estamos inicializando 

La idea de `self` en el constructor `__init__()`: En la clase calculadora estamos creando atraves del constructor un nuevo objeto, que ese objeto es `calc`, que le pasamos el valor `numero`
Una vez contemplado los valores en el constructor debemos crear estas igualdades, para asignarle el atributo correspondiente 
Asi que le pasamos el `self.numero` para que cal.numero valga 5 asi que le ponemos `numero`

Ahora si queremos sumarle un número a ese valor de `5` podemos hacer lo siguiente 
Crear un metodo que se va llamar suma `def suma()`
Agregamos otro valor para que sume con el otro atributo `5` seria: `calc.suma(8)`, si le pasamos este nuevo valor hara referencia a todo el objeto `calc`
Hacemos referencia a `self` en el metodo suma haciendo referencia al objeto `calc` y agregarle `(otro_numero)`
Realizando esto hariamos referencia a ambos numeros para para que se sumen `{self.numero + otro_numero`

```bash
#!/usr/bin/python3

class Calculadora:
	def __init__(self, numero): # Calculadora.__init__(calc, numero)
		self.numero = numero # calc.numero = 50

	def suma(self, otro_numero): # Calculadora.suma(calc, 8)
		print(self.numero + otro_numero) # calc.numero + 8 -> 5 + 8

calc = Calculadora(50)
calc.suma(80)

```

Ahora trataremos de crear un método que nos devuelva una suma doble, le agregamos la siguiente definición para poder explicarles mejor 

Agregamos definición `def_suma():` 
Agregamos el `calc.doble_suma(2, 9)`

Para esto querremos que el número 2 nos devuleva `2 + 5` todo eso mas el `9 + 5` por separado 

llamaremos por el metodo suma en nuestra definición de `doble_suma():` para pasarle el 2 + 5 que es el atributo del self para luego llamarla del metodo suma desde el metodo doble_suma, sumara primeramente el 5 + 9 

Como se le esta pasando dos valores y estamos tratando con el objeto `calc` asi que le añadimos el `def doble_suma(self, num1, num2):` ya que son dos números los cuales les estamos pasando 

Ahora cuando queramos ingresar a otro método excistente que sean metodos de la clase y por consecuencia son metodos que podemos referenciar, atraves de el objeto, ahora nos podriamos aprovechar de `calc` que se representa por un `self.suma` y hacer lo que deseemos 

Suma recibiria el metodo `otro_numero` que recuerden que le sumamos `self.numero` como atributo que es `5`
Pero si por debajo le pasamos `self.suma(num1)` Esto haria que para la clase `Calculadora`, llamando al método `suma`, que en este caso le estariamos pasando el `self.suma(num1)` representando a `calc` y un número que en este caso seria `(num1)`, pero antes de poner `calc.suma(8)` por que es la misma referencia de la clase que estamos empleando 

Esto nos dara como resultado que si llamamos a `self.suma(num1)` vendria equivaliendo a `2` asi que por lo tanto `otro_numero` va a valer 2, y 2 lo va a sumar a `self.numero` que es 5, que seria 7 de respuesta 
Ahora quisieramos volver a llamar a `self.suma(num2)` pasando num2 que seria `9` y este numero se suma con el 5.

Para evitar errores eviten usar el `print` arriba y realicen un  `return` arriba para que el tipo de dato sea el mismo y tengamos un valor entero, realizado esto podemos usar el print pero puede que el tipo de dato cambie asi que preferible utilizar un `return en ambos lugares`

Y ya desde el final realizar el `print`
```bash
#!/usr/bin/python3

class Calculadora:
	def __init__(self, numero): # Calculadora.__init__(calc, numero)
		self.numero = numero # calc.numero = 50

	def suma(self, otro_numero): # Calculadora.suma(calc, 8)
		return(self.numero + otro_numero) # calc.numero + 8 -> 5 + 8

	def doble_suma(self, num1, num2): # Calculadora.doble_suma(calc, 2, 9)
		return self.suma(num1) + self.suma(num2)

calc = Calculadora(50)
calc.suma(80)

print(calc.doble_suma(2,9))
```

Asi que se suma el 50 + 2
Y el 80 + 9
  52
+59
111

Para entender las clases es recomendable poner representando linea por linea cada uno de las cosas 
 ejemplo:
```bash
 #!/usr/bin/python3

class Calculadora:
	def __init__(self, numero): # Calculadora.__init__(calc, numero)
		self.numero = numero # calc.numero = 50

	def suma(self, otro_numero): # Calculadora.suma(calc, 9)
		return(self.numero + otro_numero) # calc.numero + 9 -> 50 + 9 = 59

	def doble_suma(self, num1, num2): # Calculadora.doble_suma(calc, 2, 9)
		return self.suma(num1) + self.suma(num2) # calc.suma(2) + calc.suma(9) -> Calculadora.suma(calc, 2) + Calculadora.suma(calc, 9) = 59 + 52 

calc = Calculadora(50)
calc.suma(80)

print(calc.doble_suma(2,9))
```
