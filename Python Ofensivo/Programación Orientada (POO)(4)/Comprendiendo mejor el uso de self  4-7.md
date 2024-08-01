
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
		self.numero = numero # calc.numero = 5

	def suma(self, otro_numero): # Calculadora.suma(calc, 8)
		print(self.numero + otro_numero) # calc.numero + 8 -> 5 + 8

calc = Calculadora(50)
calc.suma(80)

```